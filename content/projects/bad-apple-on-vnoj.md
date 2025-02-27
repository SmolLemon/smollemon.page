+++
title = 'Bad Apple on VNOJ'
date = 2025-02-27T01:00:00+07:00
description = 'Táo hư trên VNOJ'
tags = [
	"Bad Apple",
	"Code",
	"Hướng dẫn",
]
topics = [
	"Dự án vô tri",
]
featured_image = '/images/badapple.png'
draft = false
+++

Dự án được mình làm ra vào khoảng thời gian trước kì thi HSGQG 2024 khoảng 1 - 2 tuần. 

Không hiểu sao lúc ấy mình lại nghĩ:

> Chán quá! Đi làm Bad Apple thôi!
> 
> -- Smol Lemon (2023)

Và thế là mình bắt tay vào làm Bad Apple (thay vì tập trung ôn thi :P)

Việc đầu tiên mình làm chính là tìm nơi để chơi Bad Apple. 

Mình gặp khó trong việc chọn nhưng một lúc sau mình đã có một khoảnh khắc Eureka - Chơi Bad Apple trên phần bài nộp của VNOJ!

Các pixel màu trắng sẽ là <strong><span style="color:Green">AC</span></strong>, màu đen là <strong><span style="color:Red">WA</span></strong>, số lượng testcase và số lượng **AC**, **WA** mỗi testcase hiển thị lần lượt là chiều rộng và chiều dài của khung Bad Apple và Boom!!! - Một Video Bad Apple hoàn chỉnh!

Bước thứ hai, tìm bài có số lượng testcase phù hợp.

Bài mà mình chọn chính là [Beginner Free Contest 41 - ONEDIVK](https://oj.vnoi.info/problem/fcb041_onedivk). Với 25 testcase, số lượng AC, WA của một testcase theo tỉ lệ với video gốc sẽ là 33, con số phù hợp để làm video - không quá lớn, không quá nhỏ.

Bước thứ ba, tách các pixel của video gốc ra file JSON.

Bước này là bước khó nhất trong dự án vì các bước khá lằng nhằng. Mình đã làm các các bước nhỏ như sau:
- Tải Video Bad Apple
- Tách từng frame một từ Video
- Giảm độ phân giải từng frame xuống thành 33x25
- Kiểm tra *từng pixel* của *từng frame*.
- Viết kết quả vào file JSON.

Với bước 1 mình sử dụng [FFMPEG](https://ffmpeg.org/) tách ra thành từng frame `Original/frame_[frame_num].png`. Kết quả có 6572 khung hình!!!.

```shell
$ ffmpeg -i badapple.mp4 'Original/frame_%04d.png'
```

Bước 2 mình sử dụng lệnh từ [ImageMagick](https://imagemagick.org/) thay đổi độ phân giải của các frame và viết một chương trình C++ nhỏ để thực hiện lệnh cho từng frame một.

```C++
	system(("convert -resize 33x25 Original/frame_" + frame_num + ".png Low_Res_33x25/frame_" + frame_num + ".png").c_str());
```

Đối với 3 bước cuối cùng mình viết một chương trình Python cùng thư viện [openCV](https://opencv.org/). Nếu như màu của pixel từ [0, 127] thì viết vào file JSON số 0, khoảng còn lại là số 1.

Và thế là xong, đã có file JSON hơn 10MB dùng để chơi Bad Apple!

Bước thứ tư chính là viết chương trình JS để chỉnh sửa trang. Có thể nhìn qua code tại [Codeberg](https://codeberg.org/SmolLemon/Bad-Apple/src/branch/main/userscript.js) hoặc [Github](https://github.com/SmolLemon/Bad-Apple/blob/main/userscript.js) để hiểu thêm.

Bước cuối cùng chính là quay video và đăng lên Youtube.

Bad apple chạy với 30 fps, và trong lúc chạy thử thì trình duyệt trên máy mình đã load không kịp theo thời gian thực (rất là lag) để quay lên mình quyết định giảm xuống còn 10fps, và edit video chạy x3 tốc độ.

Thành quả cuối cùng:

{{< youtube mzbvxjmd21Q >}}

Tổng kết:

Vì đây cũng là video nhiều view nhất trên kênh youtube của mình (938 view, 42 like tại thời điểm viết bài viết) nên mình cũng khá tự hào với dự án này. Những gì mình học được qua dự án này không rất có ích và không hề bị lãng phí.

Chào tạm biệt, cảm ơn vì đã đọc bài viết này!