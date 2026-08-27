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

# Phase 15 — Requirement Compliance & Submission Gate

## Mục tiêu
Đảm bảo game đáp ứng đầy đủ các yêu cầu bắt buộc trước khi tối ưu dung lượng.

> Dung lượng xếp hạng phải được đo trên toàn bộ artifact nộp, theo đúng luật submit.

## Tasks
- [ ] Game chạy được trực tiếp trên browser.
- [ ] Player điều khiển được tank và bắn.
- [ ] Enemy có AI và có thể bắn.
- [ ] Có collision, map/wall, HP, score, wave và difficulty scaling.
- [ ] Có Game Over và Restart.
- [ ] Có Settings và thay đổi được trong game.
- [ ] Có ít nhất 2 màn chơi.
- [ ] Có flow Level 1 → Level 2 → Final Win.
- [ ] Có điều kiện Lose.
- [ ] Không còn requirement bắt buộc nào chưa đáp ứng.

## Output bắt buộc
Requirement checklist PASS và demo được toàn bộ flow.

---

# Phase 16 — Main Menu, Settings & UI Validation

## Mục tiêu
Hoàn thiện UI tối thiểu với chi phí byte thấp.

## Tasks
### Main Menu
```text
TANK GAME
[ PLAY ]
[ SETTINGS ]
[ HOW TO PLAY ]
```

### Settings
```text
Difficulty: [Easy / Normal / Hard]
Sound: [ON / OFF]
Controls: WASD + Mouse
```

### HUD
```text
HP / LIVES | SCORE | LEVEL
```

### Win / Lose
```text
YOU WIN → NEXT LEVEL / RESTART
YOU LOSE → RETRY / MENU
```

## Acceptance Criteria
- [ ] Menu hoạt động.
- [ ] Settings hoạt động.
- [ ] HUD hiển thị thông tin cần thiết.
- [ ] Win/Lose hoạt động.
- [ ] Không thêm UI framework hoặc asset ngoài.

## Output bắt buộc
Menu → Settings → Level 1 → Level 2 → Win/Lose.

---

# Phase 17 — Multi-Level Gameplay

## Mục tiêu
Đảm bảo requirement tối thiểu 2 màn rõ ràng và có progression.

## Tasks
- [ ] Level 1 có map/bố cục và độ khó riêng.
- [ ] Level 2 có map/bố cục và độ khó cao hơn.
- [ ] Hạ toàn bộ enemy ở Level 1 → Level 2.
- [ ] Hạ toàn bộ enemy ở Level 2 → Final Win.
- [ ] Restart reset level, score, HP và enemy.

## Output bắt buộc
Hai level chơi được từ đầu đến cuối.

## Acceptance Criteria
- [ ] Level 1 PASS.
- [ ] Level 2 PASS.
- [ ] Transition PASS.
- [ ] Final Win PASS.

---

# Phase 18 — Offline & Clean-Machine Validation

## Mục tiêu
Xác nhận game không phụ thuộc Internet hoặc môi trường development.

## Tasks
- [ ] Audit không có CDN, API, fetch/network runtime, external script/CSS/image/font.
- [ ] Tắt Internet và chạy toàn bộ flow.
- [ ] Test trên browser profile sạch/incognito hoặc máy sạch.
- [ ] Không cần npm install, Python, server, database hoặc runtime đặc biệt.

## Output bắt buộc
```text
Offline: PASS
Clean browser: PASS
No external dependency: PASS
```

---

# Phase 19 — Submission Packaging

## Mục tiêu
Tạo artifact nộp nhỏ nhất nhưng đúng format đề.

## Tasks
- [ ] Có bản chạy được.
- [ ] Có `src/` nếu luật submit yêu cầu source.
- [ ] Có README nếu luật submit yêu cầu.
- [ ] Loại `node_modules/`, `.git/`, IDE config, cache, source map, log, temp và file trùng.
- [ ] Xác nhận chính xác artifact nào được dùng để xếp hạng dung lượng.

## Output bắt buộc
```text
submission/
└── <artifact chạy được>
```

> Theo plan hiện tại, phương án tối giản ưu tiên một `index.html` duy nhất nếu luật cho phép.

---

# Phase 20 — Final Size Optimization

## Mục tiêu
Tối ưu dung lượng artifact cuối cùng, không chỉ source.

## Tasks
- [ ] Đo baseline.
- [ ] Minify HTML/CSS/JS.
- [ ] Remove comments, whitespace và dead code.
- [ ] Rút gọn identifier khi có lợi.
- [ ] Rút gọn data/map representation.
- [ ] Không giữ asset/dependency không cần thiết.
- [ ] Thử compression phù hợp nếu submit dưới dạng ZIP.
- [ ] Đo lại sau từng nhóm thay đổi.

## Metrics
```text
Before: XX bytes
After:  XX bytes
Saved:  XX bytes
Reduction: XX%
```

## Output bắt buộc
Artifact nhỏ nhất đạt được mà vẫn PASS toàn bộ requirement.

---

# Phase 21 — Aggressive Optimization / Code Golf

## Mục tiêu
Tối đa hóa gameplay trên mỗi byte.

## Tasks
- [ ] Inline function nhỏ nếu giảm byte.
- [ ] Gộp state/data.
- [ ] Simplify rendering bằng Canvas primitive.
- [ ] Simplify enemy AI nhưng vẫn giữ behavior bắt buộc.
- [ ] Loại feature không bắt buộc có byte cost cao.
- [ ] Sau mỗi optimization phải regression test.

## Quy tắc
```text
Feature → bytes added → gameplay value
Không đáng → REMOVE
Đáng → KEEP
```

## Output bắt buộc
Phiên bản nhỏ nhất nhưng vẫn playable và hợp lệ.

---

# Phase 22 — Final Regression Test

## Checklist
- [ ] Menu.
- [ ] Settings.
- [ ] Controls.
- [ ] Player movement.
- [ ] Shooting.
- [ ] Enemy AI.
- [ ] Enemy shooting.
- [ ] Collision.
- [ ] HP.
- [ ] Score.
- [ ] Wave.
- [ ] Difficulty scaling.
- [ ] Level 1.
- [ ] Level 2.
- [ ] Level transition.
- [ ] Win.
- [ ] Game Over/Lose.
- [ ] Restart.
- [ ] Offline.
- [ ] Clean browser.

## Output bắt buộc
```text
Gameplay: PASS
Settings: PASS
2+ Levels: PASS
Win/Lose: PASS
Offline: PASS
Clean machine: PASS
```

---

# Phase 23 — Final Artifact Audit

## Mục tiêu
Đảm bảo file dùng để submit chính là phiên bản đã test và đo size.

## Tasks
- [ ] Mở artifact final.
- [ ] Chơi lại ít nhất Level 1 và Level 2.
- [ ] Test Win và Lose.
- [ ] Test Settings.
- [ ] Test offline.
- [ ] Kiểm tra không có file thừa.
- [ ] Kiểm tra filename đúng format.
- [ ] Đo chính xác size cuối cùng.
- [ ] Không sửa artifact sau lần đo cuối; nếu sửa phải đo lại.

## Output bắt buộc
```text
READY_TO_SUBMIT
Size: XX bytes
Requirements: PASS
Offline: PASS
Clean machine: PASS
```

---

# Phase 24 — Submission

## Tasks
- [ ] Upload đúng channel/nơi submit theo đề.
- [ ] Upload đúng artifact final.
- [ ] Kèm screenshot nếu đề yêu cầu.
- [ ] Comment cách chạy + controls + settings + số màn + dung lượng.
- [ ] Kiểm tra lại file sau khi upload.

## Output cuối cùng
```text
Submission
├── final artifact
├── screenshot (nếu yêu cầu)
└── submission comment
```

---

# Phase 25 — Final Definition of Done

## Requirement Gate
- [ ] Game chạy được.
- [ ] Player điều khiển và bắn.
- [ ] Enemy AI và enemy shooting.
- [ ] Collision/map/HP/score/wave/difficulty scaling.
- [ ] Settings.
- [ ] ≥ 2 levels.
- [ ] Win/Lose/Game Over.
- [ ] Restart.

## Technical Gate
- [ ] Browser game.
- [ ] Offline.
- [ ] Không external dependency/asset.
- [ ] Không backend/database.
- [ ] Single-file nếu luật cho phép.

## Size Gate
- [ ] Minified.
- [ ] Không dead code/file thừa.
- [ ] Đã đo artifact cuối.
- [ ] Đã regression test sau optimization.

## Submission Gate
- [ ] Đúng format.
- [ ] Đúng filename.
- [ ] Đúng artifact.
- [ ] Đã kiểm tra final size.

---

# Phase 26 — Final Flow

```text
GAMEPLAY COMPLETE
       ↓
REQUIREMENT CHECK
       ↓
MENU + SETTINGS + UI
       ↓
2+ LEVELS
       ↓
WIN / LOSE
       ↓
OFFLINE + CLEAN-MACHINE TEST
       ↓
PACKAGE
       ↓
MINIFY
       ↓
MEASURE SIZE
       ↓
CODE GOLF
       ↓
REGRESSION TEST
       ↓
MEASURE AGAIN
       ↓
FREEZE FINAL ARTIFACT
       ↓
SUBMIT
```

## Nguyên tắc cuối cùng
> **Pass requirement trước, tối ưu byte sau.**

> **Mục tiêu: game playable tốt nhất trên mỗi byte dung lượng.**
