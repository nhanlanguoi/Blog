---
title: "Tiến trình & Luồng"
date: "2025-04-28"
updated: "2023-04-28"
categories:
  - "sveltekit"
  - "markdown"
  - "svelte"
coverImage: "/images/tientrinhandluong.png"
coverWidth: 16
coverHeight: 9
excerpt:  Tiến trình & Luồng.
---


# Hiệu Năng Máy Tính và Ứng Dụng Đa Luồng, Đa Tiến Trình

## 1. Kiểm Tra Hiệu Năng Máy Tính

- **Chip**: Apple M1
- **CPU**: 8 nhân (4 nhân hiệu năng cao + 4 nhân tiết kiệm điện)
- **GPU**: 7 nhân
- **RAM**: 8GB

**Hiệu năng**: Apple M1 sử dụng kiến trúc ARM và thiết kế SoC (System on a Chip), giúp các thành phần như CPU, GPU, RAM được tích hợp chung trên một chip. Điều này giúp truyền tải dữ liệu nhanh hơn, giảm độ trễ và tiết kiệm điện năng.

## 2. 12 Bài Toán Phổ Biến Trong CNTT Sử Dụng Đa Luồng, Đa Tiến Trình

| STT | Bài toán/Ứng dụng | Mô tả việc dùng đa luồng / đa tiến trình |
|-----|--------------------|------------------------------------------|
| 1 | Game online (multiplayer) | Mỗi phòng chơi là một luồng/tiến trình riêng để xử lý các người chơi độc lập. |
| 2 | Ứng dụng thương mại điện tử (Shoppe, Lazada) | Tìm kiếm, đặt hàng, thanh toán xử lý đồng thời qua các luồng khác nhau để tăng tốc độ phản hồi. |
| 3 | Trình biên dịch (Compiler) | Phân tích cú pháp, tối ưu mã, sinh mã máy có thể xử lý song song để tăng tốc biên dịch. |
| 4 | Huấn luyện mô hình Machine Learning | Dữ liệu chia batch, mỗi batch huấn luyện bởi các tiến trình khác nhau (đa tiến trình). |
| 5 | Ứng dụng ngân hàng số | Giao dịch, kiểm tra số dư, tải dữ liệu ảnh được xử lý song song bằng đa luồng. |
| 6 | Tìm đường đi ngắn nhất (AI, bản đồ) | Các thuật toán (như A*) có thể chia để chạy song song trên nhiều luồng để tăng tốc. |
| 7 | ChatGPT/Web AI | Mỗi người dùng là một tiến trình riêng để xử lý truy vấn, giữ kết nối ổn định. |
| 8 | Xử lý ảnh/video | Mỗi frame hoặc phần ảnh/video có thể xử lý song song bằng các luồng. |
| 9 | Web server (Apache, Nginx) | Mỗi request người dùng được xử lý bởi một luồng riêng biệt để tránh nghẽn. |
| 10 | Tìm kiếm văn bản (Google Search) | Mỗi luồng xử lý tìm kiếm trên một tập dữ liệu khác nhau để tăng tốc độ trả kết quả. |
| 11 | Database system (MySQL, PostgreSQL) | Truy vấn, cập nhật, ghi log... được phân chia theo luồng để đảm bảo hiệu suất và đồng bộ. |
| 12 | Ứng dụng xử lý thời gian thực (Zoom, Discord) | Âm thanh, hình ảnh, chat... được xử lý bằng các luồng riêng biệt để đảm bảo độ trễ thấp. |


## 3. Viết ra giấy rồi chụp ảnh, liệt kê các trường hợp nào thì nên dùng thread, trường hợp nào nên dùng process, khi nào thì nên dùng cả hai. Viết dưới dạng table và đưa ví dụ các bài toán




## 4. Report, tìm hiểu 1. chatGPT training tập dữ liệu lớn bằng distributed system như thế nào. Đưa link nguồn tài liệu tham khảo từ google

Do kích thước khổng lồ của mô hình và tập dữ liệu, việc huấn luyện ChatGPT yêu cầu sử dụng hệ thống phân tán để xử lý hiệu quả. Các kỹ thuật chính bao gồm:

- **Song song hóa dữ liệu (Data Parallelism)**: Chia nhỏ tập dữ liệu và huấn luyện trên nhiều GPU hoặc máy chủ song song.
- **Song song hóa mô hình (Model Parallelism)**: Chia nhỏ mô hình thành các phần và phân phối chúng trên nhiều thiết bị để xử lý đồng thời.
- **Song song hóa pipeline (Pipeline Parallelism)**: Chia quá trình huấn luyện thành các giai đoạn và xử lý chúng theo chuỗi trên các thiết bị khác nhau.

### Tham khảo:

1. [How ChatGPT and our foundation models are developed](https://help.openai.com/en/articles/7842364-how-chatgpt-and-our-foundation-models-are-developed)
2. [Wikipedia - GPT-3](https://en.wikipedia.org/wiki/GPT-3)


