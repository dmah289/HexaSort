# Giới thiệu cơ bản
- Hexa Sort thuộc thể loại Puzzle
- Gameplay chính được thiết kế xoay quanh việc trộn các stack hexa có cùng màu trên đỉnh lại với nhau
	- Người chơi đặt các stack hexa được sinh ra lên 1 ô lục giác trên lưới lục giác
	- Ô vừa được đặt stack lên sẽ bắt đầu quá trình trộn các stack với các bước:
		- Tìm kiếm hàng xóm theo 6 cạnh của hexa mà có những hexa trên đỉnh cùng màu với hexa trên đỉnh stack tại ô vừa đặt.
		- Khi đã tìm thấy tất cả hàng xóm sẽ bắt đầu trộn các hexa cùng màu trên đỉnh với nhau theo các tiêu chí được thiết kế.
		- Các ô đã đẩy stack đi sẽ tiếp tục để kiểm tra xem có thể trộn với hàng xóm của nó hay không

# Game Mechanic (Core Loop)
## Action (Core Mechanic)
- Kịch bản chuẩn
	1. Hệ thống tạo ra 1 lưới hexa và sinh ra 3 stack hexa để người chơi có thể kéo thả vào lưới
	2. Người chơi kéo thả 1 trong 3 stack hexa đang chờ để đặt lên lưới
	3. Hệ thống tìm các hàng xóm theo 6 cạnh của hexa tại ô vừa đặt mà có hexa trên đỉnh cùng màu với hexa trên đỉnh của ô vừa đặt → Nếu tìm thấy, trộn tất cả các hexa có cùng màu với nhau → Nếu trên cùng 1 stack đủ 10 hexa cùng màu trở lên, hệ thống tiến hành loại bỏ các hexa đó khỏi stack
	4. Lặp lại các bước 2 và 3 cho đến khi hết số lượng stack đang chờ, hệ thống tiếp tục sinh ra 3 stack hexa mới
	5. Lặp lại các bước 2, 3, 4 cho đến khi đạt được yêu cầu của level hiện tại.
- Win: Khi người chơi đạt đủ yêu cầu của màn chơi hiện tại
- Loss: Sau khi người chơi đặt stack lên ô cuối cùng còn trống của lưới. Hệ thống tiến hành trộng stack, khi kết thúc tiến trình này mà trên lưới không còn ô trống và người chơi chưa đạt được yêu cầu màn chơi hiện tại.

## Reward
1. Heart
	- Heart được sử dụng như lượt chơi và sử dụng thời gian để tích trữ
	- Tối đa 5 heart, mỗi heart tương ứng với thời gian chờ là 15 phút
2. Coin
	- Sau mỗi level, người chơi nhận cố định 20 coins
	- Nếu thu hồi được từ 3 stack trở lên trong 1 lần trộn, người chơi sẽ được thưởng 10 coins
	- Cũng có thể sử dụng điểm danh mỗi 1 giờ để nhận 10 coins
	- Coin chỉ được sử dụng trong việc mua lượt chơi khi bị thua (tránh việc mất heart)
3. Hexa : Hexa thu thập được trong các màn chơi được sử dụng để xây dựng các hòn đảo (tách biệt với hexa nhận được từ túi mù)
4. Túi mù
	- Người chơi tìm kiếm túi mù ngẫu nhiên khi loại bỏ được hexa khỏi stack tại 1 số màn chơi được chỉ định (Người chơi được giới thiệu về các loại túi mù tại lần đầu tiên nhận được túi mù)
	- Tại giao diện trang chủ thiết kế 4 vị trí để đặt túi mù. Túi mù được mở bằng cách đặt vào 1 trong 4 vị trí này để kích hoạt thời gian chờ, khi đã tích đủ thời gian người chơi có thể chọn vào túi mù bất cứ lúc nào để lấy vật phẩm bên trong (tối đa 3 slot vật phẩm)
	- Có 4 loại túi mù: Túi mù 1h, 2h, 8h, 1d
5. Vật phẩm hỗ trợ
	- Khi bắt đầu 1 số level được chỉ định, người chơi sẽ được mở khóa được vật phẩm hỗ trợ cho gameplay (có tutourial cho lần đầu nhận)
	- Cách 7 level kể từ level mở khóa vật phẩm sẽ nhận được thêm 1 vật phẩm hỗ trợ tương tự.

## Game Elements
1. Hệ thống phần thưởng (Xé túi mù)
	| Tên            | Hình ảnh                 | Mô tả               |
	|----------------|--------------------------|---------------------|
	| Blind Bag Hexa | ![Ảnh 1](link_ảnh)       | Người chơi sẽ nhận được hexa với màu bất kỳ và được lưu trữ lại. Trong gameplay, người chơi phải tiêu 10 coin để được sử dụng số hexa này|
	| Coin           | ![Ảnh 2](link_ảnh)       | Người chơi nhận được ngẫu nhiên 5-10 coins|
	| Items          | ![Ảnh 3](link_ảnh)       | Người chơi nhận các vật phẩm hỗ trợ cho gameplay|

	### Xác suất và số lượng phần thưởng
	| Loại / Item    | Hexa   | Coin | Items |
	|----------------|--------|------|-------|
	| 1h             | 100 / (1) | 100 / (5-7) | 0 
	| 2h             | 100 / (2-3) | 90 / (7-10) | 0
	| 8h             | 100 / (2-3) | 90 / (7-10) | 0
	| 8h             | 100 / (3) | 90 / (10) | 100 / 1
2. Hệ thống vật phẩm hỗ trợ
	| Tên            | Hình ảnh                 | Unlock Level | Mô tả               |
	|----------------|--------------------------|--------------|---------------------|
	| Hammer         | ![Ảnh 1](link_ảnh)       | 3            | Người chơi chọn 1 ô cụ thể trên lưới → 1 chiếc búa xuất hiện để đập đi stack hexa đang nằm trên ô đã được chỉ định → Ô vừa đập được coi như ô trống và có thể đặt stack hexa mới|
	| Respawn        | ![Ảnh 2](link_ảnh)       | 6            | Hệ thống hủy hết stack hexa đang chờ (bất kể số lượng) → Sinh ra 3 stack hexa mới (không có cơ chế đặc biệt)|
	| Swap           | ![Ảnh 3](link_ảnh)       | 9            | Người chơi chọn 1 stack hexa muốn đổi chỗ và kéo đến vị trí ô có stack hexa muốn đổi chỗ → Hệ thống hiển thị trước trạng thái lưới sau khi hoán đổi (Người chơi vẫn giữ stack) → Người chơi thả stack đã chọn xuống ô muốn đổi → Hệ thống hoán đổi vị trí 2 stack được chỉ định cho nhau <br> (Nếu người chơi thả lại stack về vị trí cũ, hệ thống không thực hiện thay đổi nào và vẫn giữ tiến trình của Swap)|
3. Hệ thống chướng ngại vật trên lưới
	| Tên                  | Hình ảnh                 | Mô tả               |
	|----------------------|--------------------------|---------------------|
	| Score Gate Cell      | ![Ảnh 1](link_ảnh)       | Ô được chỉ định (không có stack) hiển thị tổng số hexa tối thiểu để active. Nếu chưa đủ tổng số hexa sẽ không thể đặt stack hexa lên|
	| Freezing Trap Stack  | ![Ảnh 2](link_ảnh)       | Ô được chỉ định (có sẵn stack) được bọc bởi lớp kính do đó không thể tương tác với các stack hexa khác cho tới khi đủ tổng số hexa yêu cầu để phá kính|

# Entity Class Diagram
1. Mô tả
	- 1 lưới (ma trận) có nhiều ô
	- 1 ô chứa tối đa 1 stack
	- 1 stack chứa nhiều hexa (ít nhất 1)
2. Biểu đồ

# Core Pillar
## Sinh stack chờ
1. Các trường hợp:
	- Người chơi bắt đầu màn chơi mới
	- Người chơi bị thua trong màn chơi hiện tại
	- Người chơi đã đặt hết 3 stack chờ lên lưới (duy trì 1 biến đếm số lượng stack đã được đặt)
	> **Note** : Khi có sự thiết lập màn chơi, hệ thống sẽ khởi tạo vị trí 1 lần cho các stack chờ so với vị trí lưới của level hiện tại trước khi bắt đầu tiến hành sinh stack:
2. Cơ chế sinh stack
	- Ràng buộc: 
		- Mỗi màn chơi có số lượng màu cố định với số lượng tối thiểu là 3
		- Mỗi stack được sinh ra có từ 1-3 màu
	- Cơ chế:

		- Quản lý 1 danh sách các màu mà từ đó có thể chọn ngẫu nhiên 3 màu để sinh ra cho 1 stack chờ
			- Danh sách này được khởi tạo với 3 màu đầu tiên của level hiện tại (mỗi level có ít nhất 3 màu)
			- Danh sách sẽ được thêm 1 màu tại mỗi mốc với cách tính như sau:
				> Số màu còn lại = tổng số màu màn chơi - 3 <br> Sau mỗi khoảng là x% (tính theo tiến độ màn chơi) sẽ cập nhật thêm 1 màu vào danh sách này <br> x = 100 / (Số màu còn lại + 1)

				> Ví dụ: 1 màn chơi có tổng số màu là 6 <br> → Số màu còn lại : 6 - 3 = 3 <br> → x = 100 / (3+1) = 25 <br> →  Các mốc thêm 1 màu mới vào sẽ là 25, 50, 75 tương ứng với 3 màu cuối cùng.
		- Công thức tính xác suất 1 màu trong danh sách được chọn:
			> Tần suất xuất hiện = Tổng số hexa màu đó / Tổng số hexa trên lưới. <br> Xác suất chọn = 100 - Tần suất xuất hiện
				
## Thao tác với stack chờ
	1. Nhấc stack hexa lên
	2. Kéo stack hexa di chuyển
	3. Thả stack hexa xuống

## Trộn stack hexa
	- Khi đặt stack hexa được sinh ra xuống lưới, stack hexa này bắt đầu duyệt qua các hàng xóm theo 6 cạnh của hexa

# Tutourial
1. Màn đầu tiên
2. Phần mở rộng

# Level Editor

# Sound Design

# Triggers
1. Chiến lược quảng cáo