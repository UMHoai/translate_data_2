giúp cho các nhà phát triển và quản trị viên cơ sở dữ liệu có thể theo dõi và xác nhận các thay đổi cấu trúc cơ sở dữ liệu đã được áp dụng đúng cách hay không, từ đó giúp đảm bảo tính nhất quán và độ tin cậy của cơ sở dữ liệu.

chỉ có một phiên bản của ứng dụng được phép thực hiện các thay đổi cấu trúc cơ sở dữ liệu tại một thời điểm
Khi một phiên bản của ứng dụng muốn thực hiện các thay đổi cấu trúc cơ sở dữ liệu, nó sẽ thực hiện yêu cầu khóa bảng DATABASECHANGELOGLOCK và giải phóng khóa sau khi hoàn thành thay đổi. Các phiên bản ứng dụng khác sẽ phải đợi cho đến khi khóa này được giải phóng trước khi thực hiện các thay đổi cấu trúc cơ sở dữ liệu của riêng mình.
