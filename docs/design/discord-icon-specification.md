# MTGTools Discord Server Icon Specification

## Project Overview
- **Project**: MTGTools - "La Forge des Outils Pro"
- **Purpose**: Discord server icon for competitive Magic: The Gathering tools community
- **Brand Tagline**: "Talents Techniques × Compétiteurs = Performance Maximale"

## Design Concept: "The Forge Mark"

### Core Visual Elements
1. **Base Structure**: Stylized "M" letterform that transforms into forge/anvil shape
2. **Left Stroke**: Abstract hammer/tool silhouette
3. **Right Stroke**: Ascending data bars representing analytics
4. **Negative Space**: Creates subtle upward arrow for growth/performance
5. **Overall Shape**: Bold, geometric, modern interpretation of a forge

### Color Specifications

```css
/* Primary Palette */
--primary:    #fbbf24;  /* Yellow-400 - Main icon color */
--secondary:  #f59e0b;  /* Amber-500 - Gradient accent */
--background: #000000;  /* Black - Discord-friendly bg */
--highlight:  #fde68a;  /* Yellow-200 - Glow effects */

/* Gradient Definition */
background: linear-gradient(135deg, #fbbf24 0%, #f59e0b 100%);
```

### Size Specifications

| Size | Usage | Details |
|------|-------|---------|
| 512×512px | Source file | Full detail, all effects |
| 256×256px | Large display | Profile views |
| 128×128px | Server browser | Clear at medium size |
| 64×64px | Small display | Simplified details |
| 32×32px | Minimum size | Bold silhouette only |

### Construction Guidelines

#### Grid System
- **Base Grid**: 24×24 units
- **Padding**: 2 units from canvas edge
- **Icon Area**: 20×20 units active space
- **Alignment**: Optically centered

#### Geometric Construction
```
1. Start with Inter Black (900) "M" at 16 units height
2. Angle: 15° italic slant for dynamism
3. Stroke modifications:
   - Left stroke: Taper from 3 units to 2 units
   - Right stroke: Step pattern for data bars
   - Valley: Curved to suggest anvil base
4. Corner radius: 0.5 units on select corners
```

### Visual Hierarchy

#### Primary Read (Distance/Small)
- Yellow "M" shape on black background
- Clear forge silhouette
- High contrast for visibility

#### Secondary Read (Close/Large)
- Data visualization details in right stroke
- Gradient effects visible
- Subtle glow around edges

### Technical Specifications

#### File Formats
- **Master**: SVG vector file
- **Discord**: PNG 512×512px with transparency
- **Variants**: PNG exports at all specified sizes

#### Effects (512px version only)
```css
/* Outer glow */
filter: drop-shadow(0 0 4px rgba(251, 191, 36, 0.3));

/* Inner gradient */
fill: url(#forge-gradient);

/* Data bars pattern */
mask: url(#data-pattern);
```

### Alternative Versions

#### Version A: High Contrast
- Solid #fbbf24 yellow
- No gradients or effects
- Maximum clarity at all sizes

#### Version B: Dark Mode
- Inverted color scheme
- Black icon on yellow background
- For light theme contexts

#### Version C: Monochrome
- Single color #fbbf24
- Relies purely on shape
- Accessibility-focused

### Implementation Checklist

- [ ] Create SVG master file with proper layering
- [ ] Export PNG at all required sizes
- [ ] Test visibility on Discord dark theme
- [ ] Verify clarity at 32×32px minimum size
- [ ] Create style guide showing all versions
- [ ] Package files for easy deployment

### Usage Guidelines

#### Do's
- ✓ Use on dark backgrounds for optimal contrast
- ✓ Maintain minimum clear space of 1× icon height
- ✓ Use provided color values exactly
- ✓ Apply to Discord, social media avatars

#### Don'ts
- ✗ Alter proportions or angles
- ✗ Add additional effects or shadows
- ✗ Use on busy or patterned backgrounds
- ✗ Combine with other logos in same space

### Accessibility Notes

- **Contrast Ratio**: 12.5:1 (WCAG AAA compliant)
- **Color Blind Safe**: Shape-dependent, not color-dependent
- **Reduced Motion**: No animated versions needed

### File Naming Convention
```
mtgtools-discord-icon-512.png
mtgtools-discord-icon-256.png
mtgtools-discord-icon-128.png
mtgtools-discord-icon-64.png
mtgtools-discord-icon-32.png
mtgtools-discord-icon.svg
```

## Design Rationale

The "Forge Mark" concept perfectly captures MTGTools' essence:
- **Forge**: Represents building/creating tools together
- **Data Bars**: Technical, analytical approach
- **Upward Arrow**: Growth, improvement, performance
- **Bold "M"**: Strong brand recognition
- **Yellow/Gold**: Premium, valuable, attention-grabbing

This icon will stand out in Discord server lists while maintaining professional appeal for both developers and competitive players.