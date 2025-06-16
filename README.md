# Wedding
Source code để build website lời mời đám cưới


# Cách tạo form:
1. Tạo Google Sheet mới:
    Truy cập https://sheets.new
    Đặt tên, tạo các cột: Họ tên, Mối quan hệ, Lời chúc, Tham dự, Thời gian gửi
    Đặt tên sheet là "Đám cưới"

2. Tạo Apps Script mới: (Google > Extensions > Apps Script)
    const sheetName = 'Đám cưới';

    function doPost(e) {
    const sheet = SpreadsheetApp.getActiveSpreadsheet().getSheetByName(sheetName);
    const data = JSON.parse(e.postData.contents);

    sheet.appendRow([
        data.name,
        data.relation,
        data.message,
        data.attendance,
        new Date().toLocaleString("vi-VN", { timeZone: "Asia/Ho_Chi_Minh" })
    ]);

    return ContentService
        .createTextOutput(JSON.stringify({ result: 'success' }))
        .setMimeType(ContentService.MimeType.JSON);
    }

3. Deploy như Web App
    Vào Deploy > Manage deployments (Triển khai -> Quản lý các tùy chọn triển khai)
    Chọn Web App (Chọn loại -> Ứng dụng web)
    Mô tả: Gửi lời chúc
    Access: Anyone (Người có quyền truy cập -> Bất cứ ai)
    Bấm Deploy
    Lấy URL → gọi là GOOGLE_SCRIPT_URL

