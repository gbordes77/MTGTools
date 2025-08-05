# MTGTools Discord Icon Visual Guide

## ASCII Representation of "The Forge Mark"

### Full Size Concept (Simplified)
```
┌────────────────────────┐
│                        │
│    ╱╲        ╱╲       │
│   ╱  ╲      ╱┃┃╲      │
│  ╱    ╲    ╱┃╱┃┃╲     │
│ ╱      ╲  ╱┃╱╱┃┃┃╲    │
│╱___    _╲╱┃╱╱╱┃┃┃┃╲   │
│    ╲  ╱  ┃╱╱╱╱┃┃┃┃┃   │
│     ╲╱   ╱╱╱╱╱┃┃┃┃┃   │
│          ────────────   │
│                        │
└────────────────────────┘

Legend:
╱╲ = Stylized "M" strokes
┃  = Data bars (right stroke)
── = Anvil base (valley)
```

### Construction Breakdown

#### 1. Base "M" Shape
```
     ╱╲        ╱╲
    ╱  ╲      ╱  ╲
   ╱    ╲    ╱    ╲
  ╱      ╲  ╱      ╲
 ╱        ╲╱        ╲
```

#### 2. Left Stroke Modification (Tool/Hammer)
```
     ╱╲
    ╱  ╲     ← Tapered top
   ╱    ╲    ← Tool handle
  ╱      ╲   ← Hammer head
 ╱___     ╲  ← Flat base
```

#### 3. Right Stroke Modification (Data Bars)
```
        ╱╲
       ╱┃┃╲    ← Small bars
      ╱┃╱┃┃╲   ← Growing bars
     ╱┃╱╱┃┃┃╲  ← Larger bars
    ╱┃╱╱╱┃┃┃┃╲ ← Full height
```

#### 4. Valley Formation (Anvil)
```
    ╲    ╱
     ╲  ╱
      ╲╱     ← Meeting point
    ──────   ← Anvil surface
```

### Size Variations

#### 32×32px (Minimum Size)
```
┌────────┐
│  ╱╲╱╲  │
│ ╱ ╲╱ ╲ │
│╱──╲──╲│
└────────┘
```

#### 64×64px
```
┌──────────────┐
│   ╱╲    ╱╲  │
│  ╱  ╲  ╱┃┃╲ │
│ ╱    ╲╱┃┃┃╲ │
│╱──────────╲ │
└──────────────┘
```

### Color Application Guide

#### Primary Version
```
Background: ■ Black (#000000)
Icon:       ▨ Yellow (#fbbf24)
Accent:     ▤ Amber (#f59e0b)
```

#### Gradient Direction
```
┌────────────────┐
│ ▨▨▨▨▨▨▨▤▤▤▤▤  │  ← 135° diagonal
│ ▨▨▨▨▨▨▤▤▤▤▤▤  │     gradient from
│ ▨▨▨▨▨▤▤▤▤▤▤▤  │     yellow to amber
│ ▨▨▨▨▤▤▤▤▤▤▤▤  │
└────────────────┘
```

### Visual Effects Map

#### Glow Effect (512px only)
```
     ·····
   ··╱╲ ╱╲··
  ·╱  ╲╱  ╲·
 ·╱────────╲·
  ···········
  
· = Soft glow area
```

### Grid Alignment

#### 24×24 Grid System
```
0  4  8  12 16 20 24
┌──┬──┬──┬──┬──┬──┐
│  │  │  │  │  │  │ 4
├──┼──┼──┼──┼──┼──┤
│  │╱╲│  │╱╲│  │  │ 8
├──┼──┼──┼──┼──┼──┤
│ ╱│  ╲│╱│  ╲│ │  │ 12
├──┼──┼──┼──┼──┼──┤
│╱ │──│──│──│ ╲│  │ 16
├──┼──┼──┼──┼──┼──┤
│  │  │  │  │  │  │ 20
└──┴──┴──┴──┴──┴──┘
```

### Alternative Concepts Quick Reference

#### B: Data Forge Symbol
```
   ╱╱╱╲╲╲
  ║01010║  ← Binary flame
  ║10101║
  ╚═════╝  ← Forge base
```

#### C: MTG Hexagon
```
   ╱───╲
  ╱ ┌M┐ ╲
 │  └─┘  │
  ╲_____╱
```

#### D: Minimalist M
```
  ┌─┐ ┌─┐
  │ │ │ │
  │ ╲╱ │
  └───┘
```

## Quick Implementation Reference

1. **Primary Colors**: #fbbf24 (yellow) on #000000 (black)
2. **Minimum Size**: 32×32px with simplified design
3. **File Format**: PNG with transparency for Discord
4. **Key Feature**: "M" that reads as forge/anvil with data elements
5. **Avoid**: Complex details that disappear at small sizes

This visual guide provides a clear reference for implementing the MTGTools Discord icon across different contexts and sizes.