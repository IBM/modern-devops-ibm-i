# Modern DevOps for IBM i - Visual Architecture Guide

This document provides visual diagrams to help you understand and explain the repository structure and file interactions.

## 1. Complete Site Architecture

```mermaid
graph TB
    subgraph ROOT["🏠 Root Directory"]
        INDEX["index.html<br/>🎯 Landing Page<br/>Entry point for all users"]
        TRACK1["track1.html<br/>📚 Track 1 Overview<br/>Getting Started"]
        TRACK2["track2.html<br/>📚 Track 2 Overview<br/>Implementation"]
        STYLES["styles.css<br/>🎨 Shared Styles<br/>Used by all modules"]
        ASSETS["*.svg<br/>🖼️ Icon Assets<br/>Visual elements"]
    end

    subgraph MODULES["📦 Learning Modules"]
        direction TB
        M1["fundamentals/<br/>📖 Module 1<br/>DevOps Fundamentals"]
        M2["tools/<br/>🛠️ Module 2<br/>DevOps Tools"]
        M3["bob/<br/>🤖 Module 3<br/>IBM Bob for i"]
        M4["git/<br/>🔀 Module 4<br/>Version Control"]
    end

    subgraph CONTENT["📄 Module Content Structure"]
        direction TB
        MIDX["index.html<br/>Module Landing"]
        C1["chapter1.html<br/>Topic 1"]
        C2["chapter2.html<br/>Topic 2"]
        C3["chapter3.html<br/>Topic 3"]
        C4["chapter4.html<br/>Topic 4"]
    end

    INDEX -->|"User selects track"| TRACK1
    INDEX -->|"User selects track"| TRACK2
    TRACK1 -->|"User selects module"| M1
    TRACK1 -->|"User selects module"| M2
    TRACK1 -->|"User selects module"| M3
    TRACK1 -->|"User selects module"| M4
    
    M1 -.->|"Each module contains"| MIDX
    MIDX -->|"Sequential learning"| C1
    C1 --> C2
    C2 --> C3
    C3 --> C4
    
    M1 -.->|"Uses"| STYLES
    M2 -.->|"Uses"| STYLES
    M3 -.->|"Uses"| STYLES
    M4 -.->|"Uses"| STYLES

    style INDEX fill:#4589ff,color:#fff,stroke:#0f62fe,stroke-width:3px
    style TRACK1 fill:#d4bbff,color:#000,stroke:#8a3ffc,stroke-width:2px
    style TRACK2 fill:#d4bbff,color:#000,stroke:#8a3ffc,stroke-width:2px
    style STYLES fill:#24a148,color:#fff,stroke:#198038,stroke-width:2px
    style M1 fill:#0f62fe,color:#fff
    style M2 fill:#0f62fe,color:#fff
    style M3 fill:#0f62fe,color:#fff
    style M4 fill:#0f62fe,color:#fff
```

## 2. User Navigation Flow

```mermaid
flowchart TD
    START([👤 User Visits Site]) --> HOME[🏠 Landing Page<br/>index.html]
    
    HOME --> CHOICE{Choose Learning Path}
    CHOICE -->|Beginner| T1[📚 Track 1<br/>Getting Started<br/>track1.html]
    CHOICE -->|Advanced| T2[📚 Track 2<br/>Implementation<br/>track2.html]
    
    T1 --> MOD_CHOICE{Select Module}
    MOD_CHOICE -->|Module 1| FUND[📖 DevOps Fundamentals<br/>fundamentals/]
    MOD_CHOICE -->|Module 2| TOOLS[🛠️ DevOps Tools<br/>tools/]
    MOD_CHOICE -->|Module 3| BOB[🤖 IBM Bob<br/>bob/]
    MOD_CHOICE -->|Module 4| GIT[🔀 Git Version Control<br/>git/]
    
    FUND --> MOD_LAND[📄 Module Landing Page<br/>index.html]
    MOD_LAND --> CH1[📝 Chapter 1<br/>chapter1.html]
    CH1 --> CH2[📝 Chapter 2<br/>chapter2.html]
    CH2 --> CH3[📝 Chapter 3<br/>chapter3.html]
    CH3 --> CH4[📝 Chapter 4<br/>chapter4.html]
    
    CH4 --> COMPLETE{Continue Learning?}
    COMPLETE -->|Next Module| MOD_CHOICE
    COMPLETE -->|Back to Track| T1
    COMPLETE -->|Done| HOME

    style START fill:#8a3ffc,color:#fff
    style HOME fill:#4589ff,color:#fff
    style T1 fill:#d4bbff,color:#000
    style T2 fill:#d4bbff,color:#000
    style FUND fill:#0f62fe,color:#fff
    style TOOLS fill:#0f62fe,color:#fff
    style BOB fill:#0f62fe,color:#fff
    style GIT fill:#0f62fe,color:#fff
    style COMPLETE fill:#24a148,color:#fff
```

## 3. File Dependency Map

```mermaid
graph LR
    subgraph EXTERNAL["☁️ External Dependencies"]
        CDN_CARBON["Carbon Design System<br/>unpkg.com/carbon-components"]
        CDN_FONTS["IBM Plex Fonts<br/>Google Fonts"]
    end

    subgraph LOCAL["💾 Local Assets"]
        CSS["styles.css<br/>Shared Styles"]
        SVG["SVG Icons<br/>devops.svg, etc."]
    end

    subgraph PAGES["📄 Page Types"]
        LANDING["Landing Pages<br/>index.html<br/>track*.html"]
        MODULE["Module Pages<br/>*/index.html"]
        CHAPTER["Chapter Pages<br/>*/chapter*.html"]
    end

    CDN_CARBON -.->|"CDN Link"| LANDING
    CDN_CARBON -.->|"CDN Link"| MODULE
    CDN_CARBON -.->|"CDN Link"| CHAPTER
    
    CDN_FONTS -.->|"CDN Link"| LANDING
    CDN_FONTS -.->|"CDN Link"| MODULE
    CDN_FONTS -.->|"CDN Link"| CHAPTER
    
    CSS -->|"../styles.css"| MODULE
    CSS -->|"../styles.css"| CHAPTER
    
    SVG -.->|"Referenced"| LANDING
    SVG -.->|"Referenced"| MODULE
    SVG -.->|"Referenced"| CHAPTER

    style CDN_CARBON fill:#0f62fe,color:#fff
    style CDN_FONTS fill:#0f62fe,color:#fff
    style CSS fill:#24a148,color:#fff
    style SVG fill:#ff832b,color:#fff
```

## 4. Module Content Pattern

Each module follows this consistent structure:

```mermaid
graph TD
    subgraph MODULE["📦 Module Directory e.g., fundamentals/"]
        IDX["index.html<br/>📋 Module Overview<br/>• Lists all topics<br/>• Provides context<br/>• Links to chapters"]
        
        CH1["chapter1.html<br/>📝 Topic 1<br/>• Detailed content<br/>• Examples<br/>• Navigation"]
        
        CH2["chapter2.html<br/>📝 Topic 2<br/>• Detailed content<br/>• Examples<br/>• Navigation"]
        
        CH3["chapter3.html<br/>📝 Topic 3<br/>• Detailed content<br/>• Examples<br/>• Navigation"]
        
        CH4["chapter4.html<br/>📝 Topic 4<br/>• Detailed content<br/>• Examples<br/>• Navigation"]
        
        ICONS["*.svg<br/>🖼️ Module Icons"]
    end

    IDX -->|"Next →"| CH1
    CH1 -->|"← Back"| IDX
    CH1 -->|"Next →"| CH2
    CH2 -->|"← Back"| CH1
    CH2 -->|"Next →"| CH3
    CH3 -->|"← Back"| CH2
    CH3 -->|"Next →"| CH4
    CH4 -->|"← Back"| CH3
    CH4 -->|"← Back to Track"| TRACK[../track1.html]

    style IDX fill:#4589ff,color:#fff
    style CH1 fill:#0f62fe,color:#fff
    style CH2 fill:#0f62fe,color:#fff
    style CH3 fill:#0f62fe,color:#fff
    style CH4 fill:#0f62fe,color:#fff
    style TRACK fill:#d4bbff,color:#000
```

## 5. Page Component Structure

```mermaid
graph TB
    subgraph PAGE["📄 Typical Module/Chapter Page"]
        HEAD["<head><br/>• Meta tags<br/>• Carbon CSS CDN<br/>• IBM Plex Fonts CDN<br/>• ../styles.css link"]
        
        BODY["<body>"]
        
        CONTAINER["<div class='docs-container'>"]
        
        SIDEBAR["<nav class='sidebar'><br/>📑 Left Navigation<br/>• Module title<br/>• Topic list<br/>• Active indicator<br/>• Resources"]
        
        MAIN["<main class='main-content'>"]
        
        BREADCRUMB["<div class='breadcrumb'><br/>🏠 Home / Track / Module / Chapter"]
        
        ARTICLE["<article><br/>📝 Main Content<br/>• Headings<br/>• Paragraphs<br/>• Lists<br/>• Code blocks<br/>• Info boxes"]
        
        NAV["<nav class='page-nav'><br/>⬅️ Back | Next ➡️"]
    end

    HEAD --> BODY
    BODY --> CONTAINER
    CONTAINER --> SIDEBAR
    CONTAINER --> MAIN
    MAIN --> BREADCRUMB
    MAIN --> ARTICLE
    MAIN --> NAV

    style HEAD fill:#e0e0e0,color:#000
    style SIDEBAR fill:#f4f4f4,color:#000
    style BREADCRUMB fill:#0f62fe,color:#fff
    style ARTICLE fill:#fff,color:#000,stroke:#0f62fe,stroke-width:2px
    style NAV fill:#24a148,color:#fff
```

## 6. Styling Architecture

```mermaid
graph LR
    subgraph STYLING["🎨 Styling System"]
        direction TB
        
        CARBON["Carbon Design System<br/>• Grid system<br/>• Typography<br/>• Components<br/>• Colors"]
        
        SHARED["styles.css<br/>• Layout<br/>• Sidebar<br/>• Navigation<br/>• Content styles"]
        
        INLINE["Inline Styles<br/>• Hero sections<br/>• Custom grids<br/>• Page-specific"]
    end

    subgraph APPLY["Applied To"]
        direction TB
        LAND["Landing Pages<br/>Use: Carbon + Inline"]
        TRACK["Track Pages<br/>Use: Carbon + Inline"]
        MOD["Module Pages<br/>Use: Carbon + Shared"]
        CHAP["Chapter Pages<br/>Use: Carbon + Shared"]
    end

    CARBON -.-> LAND
    CARBON -.-> TRACK
    CARBON -.-> MOD
    CARBON -.-> CHAP
    
    INLINE -.-> LAND
    INLINE -.-> TRACK
    
    SHARED -.-> MOD
    SHARED -.-> CHAP

    style CARBON fill:#0f62fe,color:#fff
    style SHARED fill:#24a148,color:#fff
    style INLINE fill:#ff832b,color:#fff
```

## 7. Content Contributor Workflow

```mermaid
flowchart TD
    START([🚀 Start Task]) --> TASK{What to Create?}
    
    TASK -->|New Module| NEW_MOD[📦 Create New Module]
    TASK -->|New Chapter| NEW_CH[📝 Add New Chapter]
    TASK -->|Edit Content| EDIT[✏️ Edit Existing Content]
    
    NEW_MOD --> STEP1[1️⃣ Create directory<br/>mkdir new-module/]
    STEP1 --> STEP2[2️⃣ Copy template files<br/>from existing module]
    STEP2 --> STEP3[3️⃣ Update module index.html<br/>• Title<br/>• Topics<br/>• Navigation]
    STEP3 --> STEP4[4️⃣ Create chapter files<br/>chapter1-4.html]
    STEP4 --> STEP5[5️⃣ Update track page<br/>Add module card]
    STEP5 --> TEST
    
    NEW_CH --> CH1[1️⃣ Copy chapter template]
    CH1 --> CH2[2️⃣ Update content<br/>• Title<br/>• Article<br/>• Breadcrumb]
    CH2 --> CH3[3️⃣ Update navigation<br/>• Previous chapter<br/>• Module index<br/>• Sidebar]
    CH3 --> TEST
    
    EDIT --> ED1[1️⃣ Locate file<br/>Use hierarchy]
    ED1 --> ED2[2️⃣ Edit article content<br/>Keep structure]
    ED2 --> ED3[3️⃣ Maintain navigation<br/>Don't break links]
    ED3 --> TEST
    
    TEST{✅ Test Checklist}
    TEST -->|Pass| DONE([✨ Complete])
    TEST -->|Fail| FIX[🔧 Fix Issues]
    FIX --> TEST
    
    TEST -.->|Check| T1[Links work?]
    TEST -.->|Check| T2[Breadcrumbs correct?]
    TEST -.->|Check| T3[Navigation works?]
    TEST -.->|Check| T4[Responsive layout?]
    TEST -.->|Check| T5[Icons load?]

    style START fill:#8a3ffc,color:#fff
    style DONE fill:#24a148,color:#fff
    style TEST fill:#ff832b,color:#fff
    style NEW_MOD fill:#0f62fe,color:#fff
    style NEW_CH fill:#0f62fe,color:#fff
    style EDIT fill:#0f62fe,color:#fff
```

## 8. Quick Reference: Common Paths

### From Root Level
```
index.html                    → Landing page
track1.html                   → Track 1 overview
track2.html                   → Track 2 overview
styles.css                    → Shared styles
fundamentals/index.html       → Module 1 landing
```

### From Module Level (e.g., fundamentals/)
```
index.html                    → Module landing
chapter1.html                 → First topic
../track1.html                → Back to track
../styles.css                 → Shared styles
../devops.svg                 → Root-level icon
```

### From Chapter Level (e.g., fundamentals/chapter1.html)
```
index.html                    → Module landing
chapter2.html                 → Next chapter
../track1.html                → Back to track
../styles.css                 → Shared styles
../index.html                 → Site home
```

## 9. Responsive Behavior

```mermaid
graph LR
    subgraph DESKTOP["🖥️ Desktop > 1056px"]
        D_SIDE["Left Sidebar<br/>Visible"]
        D_MAIN["Main Content<br/>Center"]
        D_RIGHT["Right Sidebar<br/>Optional"]
    end

    subgraph TABLET["📱 Tablet 672-1056px"]
        T_SIDE["Left Sidebar<br/>Hidden"]
        T_MAIN["Main Content<br/>Full Width"]
    end

    subgraph MOBILE["📱 Mobile < 672px"]
        M_STACK["Stacked Layout<br/>Single Column"]
    end

    DESKTOP -->|"Resize"| TABLET
    TABLET -->|"Resize"| MOBILE
    MOBILE -->|"Resize"| TABLET
    TABLET -->|"Resize"| DESKTOP

    style DESKTOP fill:#0f62fe,color:#fff
    style TABLET fill:#8a3ffc,color:#fff
    style MOBILE fill:#d4bbff,color:#000
```

## Legend

| Icon | Meaning |
|------|---------|
| 🏠 | Home/Landing page |
| 📚 | Learning track |
| 📦 | Module directory |
| 📖 | Module content |
| 📝 | Chapter/Topic |
| 🎨 | Styling/CSS |
| 🖼️ | Images/Icons |
| ☁️ | External/CDN |
| 💾 | Local files |
| 🔀 | Version control |
| 🛠️ | Tools |
| 🤖 | AI/Bob |
| ⬅️➡️ | Navigation |
| ✅ | Testing/Complete |

## Color Coding

- **Blue (#4589ff, #0f62fe)**: Primary pages and navigation
- **Purple (#d4bbff, #8a3ffc)**: Learning tracks
- **Green (#24a148)**: Shared resources and completion
- **Orange (#ff832b)**: Warnings and special attention
- **Gray (#f4f4f4, #e0e0e0)**: Neutral elements

---

**Use these diagrams to:**
- Explain the site structure to new contributors
- Plan new content additions
- Understand file relationships
- Debug navigation issues
- Present the architecture to stakeholders