# Tech Stack & Size Optimization

## Tech stack

- **HTML:** Canvas 2D làm vùng chơi.
- **CSS:** CSS inline tối thiểu cho Canvas toàn màn hình.
- **JavaScript:** Vanilla JS cho game loop, input, tank, bullet, enemy, collision, map, score và level.
- **Dependency:** 0. Không framework, backend, database, engine, image, audio hoặc font ngoài.
- **Runtime:** Mở trực tiếp bằng trình duyệt, chạy offline.

## Cấu trúc

- `index.html`: source dễ đọc để phát triển.
- `dist/index.html`: bản minify để chạy thử/phát hành.
- `submission/index.html`: artifact cuối dùng để nộp.

## Tối ưu dung lượng

1. Giữ đồ họa bằng Canvas primitive: `fillRect`, `arc`, `rotate`.
2. Inline CSS và JavaScript để tạo một file duy nhất.
3. Xóa comment, whitespace, dead code và file không dùng.
4. Rút gọn identifier và map data sau khi gameplay đã ổn định.
5. Không dùng asset hoặc thư viện bên ngoài.
6. Đo byte trước/sau mỗi nhóm thay đổi.
7. Regression test sau minify/code golf.

**Ưu tiên:** gameplay đúng trước, tối ưu byte sau. Artifact cuối phải nhỏ nhưng vẫn chạy offline và đủ chức năng.
