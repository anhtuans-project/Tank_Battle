# Tank Game — Development Plan & Phase Outputs

## 1. Mục tiêu

Xây dựng một game bắn tank chạy trực tiếp trên trình duyệt, với tiêu chí quan trọng nhất:

> **Dung lượng file submit càng nhỏ càng tốt, nhưng game vẫn phải chạy ổn định và đáp ứng đầy đủ gameplay.**

### Mục tiêu kỹ thuật

- Chạy standalone trên browser.
- Không cần backend.
- Không cần database.
- Không phụ thuộc internet khi chơi.
- Không dùng game engine.
- Không dùng framework frontend.
- Không dùng asset hình ảnh/âm thanh bên ngoài.
- Ưu tiên Canvas 2D.
- Ưu tiên một file `index.html` duy nhất khi submit.
- Tối ưu mạnh kích thước file cuối cùng.

### Tech stack

| Thành phần | Công nghệ |
|---|---|
| UI | HTML |
| Rendering | HTML5 Canvas 2D |
| Logic | Vanilla JavaScript |
| Styling | CSS tối thiểu |
| Build | Không bắt buộc |
| Dependency | 0 |
| Backend | Không có |
| Database | Không có |
| Image asset | Không có |
| Audio asset | Không có |
| Game engine | Không có |
| Submission | Single `index.html` |

---

# 2. Nguyên tắc phát triển

## 2.1. Ưu tiên gameplay trước dung lượng

Thứ tự:

```text
Game chạy được
    ↓
Gameplay hoàn chỉnh
    ↓
Test lỗi
    ↓
Tối ưu code
    ↓
Minify
    ↓
Đo dung lượng
    ↓
Code golf nếu cần
```

Không tối ưu byte quá sớm vì sẽ làm code khó phát triển.

## 2.2. Không thêm dependency nếu không bắt buộc

Không sử dụng:

- React
- Vue
- Angular
- Phaser
- PixiJS
- Three.js
- Unity
- Godot
- Bootstrap
- Tailwind
- Lodash
- jQuery
- npm package không cần thiết

## 2.3. Không sử dụng asset ngoài

Không dùng:

- PNG
- JPG
- SVG file
- WebP
- MP3
- WAV
- custom font

Đồ họa được vẽ trực tiếp bằng Canvas API.

---

# 3. Kiến trúc tổng thể

```text
index.html
│
├── HTML
│   └── Canvas
│
├── CSS
│   └── Minimal UI
│
└── JavaScript
    │
    ├── Game Loop
    ├── Input
    ├── Player
    ├── Enemy
    ├── Bullet
    ├── Collision
    ├── Map
    ├── Game Manager
    └── Renderer
```

### Game loop

```text
Input
  ↓
Update
  ↓
Collision
  ↓
Render
  ↓
requestAnimationFrame
  ↓
Input
```

---

# Phase 1 — Project Initialization

## Mục tiêu

Tạo project tối thiểu để game có thể chạy trên browser.

## Tasks

### Task 1.1 — Tạo project

Cấu trúc ban đầu:

```text
tank-game/
└── index.html
```

### Task 1.2 — Tạo Canvas

- Tạo Canvas.
- Canvas chiếm khu vực chơi.
- Xác định width/height.
- Xóa các cấu hình không cần thiết.

### Task 1.3 — Khởi tạo game loop

Sử dụng:

```javascript
requestAnimationFrame()
```

### Task 1.4 — Game state cơ bản

Định nghĩa các trạng thái:

```text
PLAYING
GAME_OVER
```

## Output bắt buộc

```text
index.html
```

Game mở được trên browser và hiển thị Canvas.

## Acceptance Criteria

- [ ] Mở `index.html` không lỗi.
- [ ] Canvas hiển thị.
- [ ] `requestAnimationFrame()` hoạt động.
- [ ] Không có dependency bên ngoài.
- [ ] Không cần internet.

---

# Phase 2 — Player Tank

## Mục tiêu

Tạo tank người chơi và điều khiển được.

## Tasks

### Task 2.1 — Player state

Player tối thiểu có:

```text
x
y
angle
speed
hp
cooldown
```

### Task 2.2 — Keyboard input

Hỗ trợ:

```text
W / ↑
S / ↓
A / ←
D / →
```

### Task 2.3 — Movement

- Di chuyển tiến.
- Di chuyển lùi.
- Xoay trái.
- Xoay phải.

### Task 2.4 — Render tank

Không dùng image.

Vẽ bằng Canvas:

```text
Body    → rectangle
Turret  → rectangle
```

### Task 2.5 — Boundary

Tank không được đi ra ngoài vùng chơi.

## Output bắt buộc

Game có tank người chơi và có thể điều khiển bằng keyboard.

## Acceptance Criteria

- [ ] Tank hiển thị.
- [ ] Tank di chuyển.
- [ ] Tank xoay.
- [ ] Tank không đi ra ngoài màn hình.
- [ ] Không sử dụng image asset.

---

# Phase 3 — Shooting System

## Mục tiêu

Cho player bắn đạn.

## Tasks

### Task 3.1 — Mouse input

Lấy:

```text
mouseX
mouseY
```

### Task 3.2 — Aiming

Tính góc:

```javascript
dx = mouseX - tankX
dy = mouseY - tankY
angle = Math.atan2(dy, dx)
```

### Task 3.3 — Bullet entity

Bullet tối thiểu:

```text
x
y
vx
vy
owner
```

### Task 3.4 — Fire

Click chuột:

```text
Mouse click
    ↓
Check cooldown
    ↓
Create bullet
    ↓
Add to bullets[]
```

### Task 3.5 — Bullet movement

Mỗi frame:

```text
x += vx
y += vy
```

### Task 3.6 — Remove bullet

Nếu bullet ra ngoài Canvas:

```text
remove bullet
```

## Output bắt buộc

Player có thể ngắm và bắn đạn.

## Acceptance Criteria

- [ ] Mouse aim hoạt động.
- [ ] Click để bắn.
- [ ] Đạn bay đúng hướng.
- [ ] Có fire cooldown.
- [ ] Đạn được remove khi ra ngoài màn hình.

---

# Phase 4 — Enemy System

## Mục tiêu

Tạo enemy tank và AI cơ bản.

## Tasks

### Task 4.1 — Enemy entity

Enemy có:

```text
x
y
angle
speed
hp
cooldown
```

### Task 4.2 — Spawn enemy

Tạo:

```javascript
spawnEnemy()
```

Enemy xuất hiện ở vị trí ngẫu nhiên.

### Task 4.3 — Enemy AI

AI tối giản:

```text
Find player
    ↓
Calculate dx/dy
    ↓
Rotate toward player
    ↓
Move toward player
```

### Task 4.4 — Enemy shooting

Enemy có thể bắn player.

### Task 4.5 — Enemy HP

Ví dụ:

```text
hp = 2
```

Khi bị bắn:

```text
hp--
```

Khi:

```text
hp <= 0
```

enemy bị destroy.

## Output bắt buộc

Có enemy tank tự động di chuyển và bắn player.

## Acceptance Criteria

- [ ] Enemy spawn.
- [ ] Enemy tìm player.
- [ ] Enemy di chuyển.
- [ ] Enemy hướng về player.
- [ ] Enemy bắn.
- [ ] Enemy có HP.
- [ ] Enemy có thể chết.

---

# Phase 5 — Collision System

## Mục tiêu

Xử lý va chạm mà không sử dụng physics engine.

## Tasks

### Task 5.1 — Bullet → Enemy

Kiểm tra khoảng cách:

```text
distance(bullet, enemy) < collisionRadius
```

### Task 5.2 — Bullet → Player

Tương tự.

### Task 5.3 — Tank → Wall

Sử dụng collision rectangle đơn giản.

### Task 5.4 — Bullet → Wall

Bullet có thể:

- biến mất khi chạm wall;
- hoặc wall chặn bullet.

## Output bắt buộc

Hệ thống collision hoàn chỉnh cho gameplay cơ bản.

## Acceptance Criteria

- [ ] Bullet hit enemy.
- [ ] Enemy mất HP.
- [ ] Enemy chết khi HP = 0.
- [ ] Enemy bullet hit player.
- [ ] Player mất HP.
- [ ] Tank không xuyên wall.
- [ ] Bullet xử lý đúng khi chạm wall.

---

# Phase 6 — Map System

## Mục tiêu

Tạo map bằng dữ liệu thay vì image asset.

## Tasks

### Task 6.1 — Tile map

Dùng array:

```javascript
[
  [1,1,1,1,1,1],
  [1,0,0,0,0,1],
  [1,0,1,0,1,1],
  [1,0,0,0,0,1],
  [1,1,1,1,1,1]
]
```

Quy ước:

```text
0 = empty
1 = wall
```

### Task 6.2 — Render map

Vẽ wall bằng:

```javascript
ctx.fillRect()
```

### Task 6.3 — Map collision

Kiểm tra tank/bullet với wall.

### Task 6.4 — Spawn point

Đảm bảo player và enemy không spawn bên trong wall.

## Output bắt buộc

Một map chơi được với wall và collision.

## Acceptance Criteria

- [ ] Map hiển thị.
- [ ] Wall hoạt động.
- [ ] Player không xuyên wall.
- [ ] Enemy không xuyên wall.
- [ ] Bullet tương tác đúng với wall.

---

# Phase 7 — Game Rules & Progression

## Mục tiêu

Biến prototype thành game có vòng lặp chơi hoàn chỉnh.

## Tasks

### Task 7.1 — Score

Enemy chết:

```text
score += 10
```

### Task 7.2 — Wave

Ví dụ:

```text
Wave 1 → 3 enemies
Wave 2 → 5 enemies
Wave 3 → 8 enemies
```

### Task 7.3 — Difficulty scaling

Sau mỗi wave:

```text
enemy speed ↑
enemy fire rate ↑
enemy HP ↑
```

### Task 7.4 — Player HP

Ví dụ:

```text
HP = 100
```

### Task 7.5 — Game Over

```text
player.hp <= 0
        ↓
GAME OVER
```

### Task 7.6 — Restart

Cho phép:

```text
RESTART
```

để bắt đầu lại game.

## Output bắt buộc

Một game loop hoàn chỉnh:

```text
Start
 ↓
Fight
 ↓
Kill enemies
 ↓
Increase score
 ↓
Next wave
 ↓
Increase difficulty
 ↓
Player dies
 ↓
Game Over
 ↓
Restart
```

## Acceptance Criteria

- [ ] Score hoạt động.
- [ ] Wave hoạt động.
- [ ] Difficulty tăng.
- [ ] Player có HP.
- [ ] Game Over hoạt động.
- [ ] Restart hoạt động.

---

# Phase 8 — Minimal UI

## Mục tiêu

Hiển thị thông tin cần thiết nhưng không làm file phình lên.

## Tasks

### Task 8.1 — Score

Hiển thị:

```text
SCORE: 120
```

### Task 8.2 — HP

Hiển thị:

```text
HP: 80
```

### Task 8.3 — Wave

Hiển thị:

```text
WAVE: 3
```

### Task 8.4 — Game Over

Hiển thị:

```text
GAME OVER
RESTART
```

## Nguyên tắc

Không tạo UI framework.

Ưu tiên:

```text
Canvas text
```

thay vì nhiều DOM element.

## Output bắt buộc

UI tối thiểu nhưng đủ để người chơi hiểu trạng thái game.

## Acceptance Criteria

- [ ] Score hiển thị.
- [ ] HP hiển thị.
- [ ] Wave hiển thị.
- [ ] Game Over hiển thị.
- [ ] Restart hoạt động.
- [ ] Không thêm UI library.

---

# Phase 9 — Gameplay Polish

## Mục tiêu

Cải thiện cảm giác chơi nhưng vẫn kiểm soát dung lượng.

## Tasks

### Task 9.1 — Hit effect

Khi enemy chết:

```text
small explosion
```

Dùng Canvas shape, không dùng image.

### Task 9.2 — Muzzle flash

Khi bắn:

```text
small flash
```

### Task 9.3 — Screen feedback

Có thể thêm:

```text
damage flash
```

hoặc hiệu ứng rất nhỏ.

### Task 9.4 — Spawn balance

Điều chỉnh:

- enemy spawn;
- fire rate;
- movement speed;
- player speed;
- bullet speed.

## Output bắt buộc

Gameplay có cảm giác hoàn chỉnh hơn nhưng không sử dụng asset ngoài.

## Acceptance Criteria

- [ ] Không ảnh hưởng gameplay.
- [ ] Không thêm dependency.
- [ ] Không thêm asset.
- [ ] Dung lượng vẫn nằm trong budget.

---

# Phase 10 — Code Optimization

## Mục tiêu

Giảm kích thước source nhưng vẫn giữ khả năng debug.

## Tasks

### Task 10.1 — Remove dead code

Xóa:

- function không dùng;
- variable không dùng;
- CSS không dùng;
- HTML không dùng.

### Task 10.2 — Simplify data structures

Chỉ giữ state thực sự cần thiết.

### Task 10.3 — Reduce duplicated logic

Gộp các logic lặp lại nếu giúp giảm byte.

### Task 10.4 — Simplify rendering

Ưu tiên các Canvas API đơn giản:

```text
fillRect
arc
translate
rotate
fillText
```

### Task 10.5 — Remove unnecessary UI

Mọi UI không phục vụ gameplay đều phải xem xét loại bỏ.

## Output bắt buộc

Source code sạch và nhỏ hơn phiên bản trước.

## Metrics

Ghi lại:

```text
Before optimization: XX KB
After optimization:  XX KB
Reduction:            XX%
```

---

# Phase 11 — Single File Packaging

## Mục tiêu

Đưa toàn bộ game về một file duy nhất.

## Tasks

### Task 11.1 — Inline CSS

Từ:

```text
style.css
```

sang:

```html
<style>
...
</style>
```

### Task 11.2 — Inline JavaScript

Từ:

```text
game.js
```

sang:

```html
<script>
...
</script>
```

### Task 11.3 — Remove external references

Kiểm tra:

```text
<link>
<script src="">
<img src="">
<audio>
@import
```

và loại bỏ những thứ không cần thiết.

### Task 11.4 — Standalone test

Copy file sang máy/browser khác và mở trực tiếp.

## Output bắt buộc

```text
dist/
└── index.html
```

## Acceptance Criteria

- [ ] Chỉ còn 1 file.
- [ ] Không external dependency.
- [ ] Không external asset.
- [ ] Mở trực tiếp bằng browser.
- [ ] Game vẫn chạy bình thường.

---

# Phase 12 — Minification

## Mục tiêu

Giảm kích thước file submit.

## Tasks

### Task 12.1 — Minify HTML

Loại bỏ:

- whitespace;
- comment;
- line break không cần thiết.

### Task 12.2 — Minify CSS

Loại bỏ:

- whitespace;
- comment;
- selector dư thừa.

### Task 12.3 — Minify JavaScript

Loại bỏ:

- whitespace;
- comment;
- tên biến dài;
- code dư thừa.

### Task 12.4 — Kiểm tra sau minify

Mở file và test toàn bộ gameplay.

## Output bắt buộc

```text
dist/
└── index.html
```

với file đã minify.

## Metrics

Ghi lại:

```text
Before minify: XX bytes
After minify:  XX bytes
Saved:         XX bytes
```

---

# Phase 13 — Aggressive Optimization / Code Golf

## Mục tiêu

Đây là phase dành riêng cho cuộc thi có ranking dựa trên file size.

## Tasks

### Task 13.1 — Short variable names

Ví dụ:

```text
player
enemy
bullet
score
```

có thể rút gọn nếu không ảnh hưởng logic.

### Task 13.2 — Gộp function

Xem xét các function nhỏ có thể inline.

### Task 13.3 — Gộp state

Loại bỏ object/property không cần thiết.

### Task 13.4 — Rút gọn UI

Chỉ giữ:

```text
SCORE
HP
WAVE
GAME OVER
```

### Task 13.5 — Simplify graphics

Ưu tiên hình học đơn giản:

```text
rectangle
circle
line
```

### Task 13.6 — Simplify physics

Không sử dụng:

```text
physics engine
pathfinding
complex collision
```

nếu không cần thiết.

### Task 13.7 — Remove optional features

Nếu dung lượng là tiêu chí tuyệt đối, loại bỏ feature có tỷ lệ:

```text
byte cost / gameplay value
```

thấp.

## Output bắt buộc

Phiên bản submission nhỏ nhất nhưng vẫn đáp ứng luật chơi.

## Metrics

Theo dõi từng phiên bản:

```text
Version A: 15.2 KB
Version B: 11.7 KB
Version C:  8.9 KB
Version D:  6.4 KB
```

---

# Phase 14 — Final Testing

## Mục tiêu

Đảm bảo tối ưu dung lượng không phá game.

## Functional Test

### Player

- [ ] Spawn đúng.
- [ ] Di chuyển đúng.
- [ ] Xoay đúng.
- [ ] Không xuyên map.

### Shooting

- [ ] Aim đúng.
- [ ] Bắn đúng.
- [ ] Cooldown đúng.
- [ ] Bullet biến mất đúng.

### Enemy

- [ ] Spawn đúng.
- [ ] AI hoạt động.
- [ ] Enemy bắn.
- [ ] Enemy chết.

### Collision

- [ ] Bullet → Enemy.
- [ ] Bullet → Player.
- [ ] Tank → Wall.
- [ ] Bullet → Wall.

### Game

- [ ] Score.
- [ ] Wave.
- [ ] Difficulty.
- [ ] HP.
- [ ] Game Over.
- [ ] Restart.

### Browser

- [ ] Chrome.
- [ ] Edge.
- [ ] Firefox nếu luật yêu cầu.

### Offline

- [ ] Tắt internet.
- [ ] Mở `index.html`.
- [ ] Game vẫn chạy.

## Output bắt buộc

Một file final đã test:

```text
index.html
```

---

# Phase 15 — Submission Optimization

## Mục tiêu

Tạo artifact cuối cùng để submit.

## Checklist

- [ ] Không có `node_modules`.
- [ ] Không có package.json nếu không cần.
- [ ] Không có source map.
- [ ] Không có image.
- [ ] Không có audio.
- [ ] Không có font.
- [ ] Không có library.
- [ ] Không có external URL.
- [ ] Không có comment.
- [ ] Không có debug log.
- [ ] Không có dead code.
- [ ] HTML đã minify.
- [ ] CSS đã minify.
- [ ] JS đã minify.
- [ ] Game chạy offline.
- [ ] Game đã test clean browser.
- [ ] Đo chính xác file size.

## Output cuối cùng

```text
submission/
└── index.html
```

Đây là file duy nhất được submit nếu luật cho phép.

---

# 16. File Structure đề xuất

## Development

```text
tank-game/
│
├── src/
│   ├── game.js
│   ├── player.js
│   ├── enemy.js
│   ├── bullet.js
│   ├── collision.js
│   └── map.js
│
├── index.html
│
└── dist/
    └── index.html
```

## Submission

Chỉ:

```text
submission/
└── index.html
```

Nếu ngay từ đầu muốn tối giản tuyệt đối, có thể phát triển trực tiếp bằng:

```text
tank-game/
└── index.html
```

---

# 17. Definition of Done

Project được coi là hoàn thành khi:

1. Game chạy được trực tiếp trên browser.
2. Player điều khiển được tank.
3. Player có thể bắn.
4. Enemy có AI.
5. Enemy có thể bắn.
6. Có collision.
7. Có map/wall.
8. Có HP.
9. Có score.
10. Có wave.
11. Có difficulty scaling.
12. Có Game Over.
13. Có Restart.
14. Không cần backend.
15. Không cần database.
16. Không cần internet.
17. Không có external asset.
18. Không có external dependency.
19. Toàn bộ game nằm trong một file HTML.
20. File đã được minify.
21. File đã được test sau minify.
22. Đã đo chính xác dung lượng submission.

---

# 18. Dung lượng mục tiêu

| Milestone | Target |
|---|---:|
| Prototype | < 30 KB |
| Gameplay hoàn chỉnh | < 15 KB |
| Optimized | < 10 KB |
| Aggressive optimization | < 5 KB |
| Extreme code golf | < 3 KB |

Các mức trên là **target kỹ thuật**, không phải yêu cầu bắt buộc. Mức cuối cùng phụ thuộc vào luật chấm và mức độ gameplay phải giữ lại.

---

# 19. Chiến lược tối ưu cuối cùng

```text
                DEVELOPMENT
                     │
                     ▼
              Gameplay MVP
                     │
                     ▼
             Gameplay Complete
                     │
                     ▼
               Full Testing
                     │
                     ▼
             Remove Dependencies
                     │
                     ▼
              Remove Assets
                     │
                     ▼
              Single HTML File
                     │
                     ▼
                  Minify
                     │
                     ▼
              Measure File Size
                     │
                     ▼
              Code Golf / Optimize
                     │
                     ▼
                Re-test Game
                     │
                     ▼
             Measure Again
                     │
                     ▼
              SMALLEST VALID
                 SUBMISSION
```

## Nguyên tắc quyết định feature

Mỗi feature phải trả lời:

> **Feature này có đáng với số byte mà nó thêm vào không?**

Nếu không:

```text
REMOVE
```

Nếu có:

```text
KEEP
```

Mục tiêu cuối cùng không phải là game có nhiều tính năng nhất mà là:

> **Game playable tốt nhất trên mỗi byte dung lượng.**
