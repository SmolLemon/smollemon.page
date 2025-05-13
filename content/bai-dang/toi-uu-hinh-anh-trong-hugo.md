+++
title = 'Tối ưu hình ảnh trong Hugo'
date = 2025-04-04T00:00:00+07:00
description = 'Tối ưu hình ảnh khi sử dụng trình tạo trang Hugo'
tag = [
	'Hướng dẫn',
	'Hugo',
	'Web',
]
danh-muc = 'Hugo'
[params]
	article = true
	math = false
featured_image = '/images/hugo.png'
+++

Việc hiển thị hình ảnh trên trang web của bạn có thể ảnh hưởng đến trải nghiệm người dùng. Nếu bức ảnh của bạn được tối ưu (kích thước nhỏ hơn, định dạng `webp`, `jpg`,...) thì trang web của bạn sẽ tải nhanh hơn, đồng thời những người sử dụng dữ liệu đi động sẽ cảm ơn bạn khi trang của bạn không cần phải tải quá nhiều dữ liệu. Thay vì phải tự tối ưu thủ công từng file ảnh, ta có thể sử dụng những tính năng có sẵn trong trình tạo trang [Hugo](https://gohugo.io) để tự động hoá quá trình này.

## Hugo pipes

[Hugo pipes](https://gohugo.io/hugo-pipes/introduction/#article) là các hàm xử lí các các file trong hugo. Các file ảnh của ta sẽ nằm trong thư mục `assets/` để Hugo pipes sử dụng.

Để lấy một file ảnh, ví dụ như `image.png` trong thư mục `assets/`, ta gọi:

```go-html-template
{{ $image := resources.Get "image.png" }}
```

Bây giờ, để hiển thị file ảnh, ta chỉ cần viết:

```go-html-template
<img class="img" src="{{ $image.RelPermalink }}" alt="File ảnh">
```

Tuy nhiên, ảnh được hiển thị bằng cách trên chưa được tối ưu gì cả. 

Để thay đổi ảnh giúp giảm kích thước, chất lượng, khung hình,... ta sử dụng `images.Process`.

## `images.Process`

`images.Process` là một hàm xử lí hình ảnh với các tham số cho trước. Hàm có vô số tính năng nhưng mình sẽ chỉ tập trung một số ít tính năng mà mình sử dụng khi xây dựng trang web của mình.

### Thay đổi định dạng

Ta có thể thay đổi định dạng của file ảnh (`webp`, `jpg`, `png`, `gif`, `tiff`). Ví dụ, ta thay đổi định dạng `png` của `image.png` thành `image.jpg`:

```go-html-template
{{ $image := images.Process "jpg" }}
```

### Thay đổi kích thước

Kích thước của ảnh cũng có thể được thay đổi. Giả sử ta muốn thay đổi kích thước của `image.png` sao cho chiều rộng của ảnh là 500px:

```go-html-template
{{ $image := images.Process "resize 500x" }}
```

<br>

Ví dụ cho một thao tác xử lí hình ảnh (thay đổi định dạng):

{{< img src="/images/hugo.png" alt="ảnh gốc (PNG)" sup="Ảnh gốc (PNG)" process="">}}

{{< img src="/images/hugo.png" alt="ảnh chỉnh sửa (webp)" sup="Ảnh chỉnh sửa (WEBP)" process="webp">}}

Nếu bạn muốn tìm hiểu thêm những tính năng của `images.Process` thì bạn đọc qua thông tin về hàm trên [docs](https://gohugo.io/functions/images/process/#article).

## Tổng kết

Tính năng chỉnh sửa ảnh trên Hugo rất xịn và rất mạnh. Nếu bạn muốn tối ưu trang web bằng cách thay đổi file ảnh thì bạn rất nên sử dụng tính năng này để tự động hoá quá trình này.