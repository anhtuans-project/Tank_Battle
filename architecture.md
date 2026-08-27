Kiến trúc game

Mình đề xuất chia game thành khoảng 8 module logic.

Game
│
├── Input
│   ├── Keyboard
│   └── Mouse
│
├── Player
│   ├── position
│   ├── rotation
│   ├── hp
│   └── shoot()
│
├── Enemy
│   ├── position
│   ├── rotation
│   ├── hp
│   └── AI
│
├── Bullet
│   ├── position
│   ├── velocity
│   └── owner
│
├── Collision
│   ├── bullet-enemy
│   ├── bullet-player
│   └── tank-wall
│
├── Map
│   └── walls
│
├── Renderer
│   └── Canvas 2D
│
└── GameManager
    ├── score
    ├── spawn
    ├── game state
    └── game loop