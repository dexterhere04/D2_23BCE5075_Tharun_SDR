
# 2D-to-3D Blueprint Conversion & AI Floorplan Generation Platform  
**System Architecture Documentation**

---

## 1. Overview

This platform enables users to:
- Upload 2D blueprints and convert them into interactive 3D models
- Generate floorplans using natural language
- Walk through and explore buildings in real time using WebGL
- Collaborate with others on the same project

The architecture follows a **layered microservices approach** for scalability, flexibility, and AI-driven extensibility.

---

## 2. High-Level Architecture

The system is divided into the following layers:

1. Client Layer
2. Edge / Gateway Layer
3. Microservices Layer
4. AI / ML Pipeline
5. Data Layer

---

## 3. Client Layer

### Components

#### 1. Web App (Next.js PWA)
- Responsive UI
- User authentication
- Project management
- Upload blueprints
- Input natural language prompts
- View generated 3D models

#### 2. 3D Viewer (Three.js / Babylon.js)
- WebGL-based real-time rendering
- First-person walkthrough mode
- Lighting, shadows, and materials
- Camera navigation

#### 3. User
- Architects
- Designers
- Homeowners
- Builders

### Responsibilities
- Collect user input
- Display generated models
- Send requests to backend
- Handle real-time updates

---

## 4. Edge / Gateway Layer

### Components

#### 1. API Gateway (NGINX / Kong)
- Routes requests to appropriate services
- Rate limiting
- Authentication verification
- Request validation
- Logging

#### 2. WebSocket Server
- Real-time collaboration
- Live model updates
- Cursor tracking
- Multi-user synchronization

#### 3. CDN (CloudFront / Cloudflare)
- Static asset delivery
- Model caching
- Faster global access

---

## 5. Microservices Layer

Each service is independently deployable and scalable.

---

### 5.1 Blueprint Processing Service

#### Purpose
Converts raw blueprint images or CAD exports into structured data.

#### Responsibilities
- Image cleanup and normalization
- Edge detection
- Line detection
- OCR for dimensions and labels
- Scale detection
- Element extraction

#### Inputs
- Scanned blueprints
- CAD exports
- Floorplan images

#### Outputs
- Walls
- Doors
- Windows
- Room boundaries
- Dimensions

---

### 5.2 NLP Service

#### Purpose
Transforms natural language descriptions into structured layout intent.

#### Responsibilities
- Room extraction
- Constraint detection
- Relationship inference
- Style interpretation
- Layout schema generation

#### Example Input
"Create a 2BHK apartment with an open kitchen and a balcony"

#### Example Output
```json
{
  "rooms": [
    {"type": "bedroom", "count": 2},
    {"type": "kitchen", "style": "open"},
    {"type": "balcony", "attachedTo": "living room"}
  ]
}
```

---

### 5.3 2D → 3D Engine

#### Purpose
Converts 2D layout representations into 3D spatial structures.

#### Responsibilities
- Wall extrusion
- Ceiling and floor generation
- Room volume creation
- Door/window cutouts
- Collision detection
- Structural consistency checks

#### Inputs
- Blueprint processing output
- NLP layout schema

#### Outputs
- 3D geometry graph
- Spatial relationships

---

### 5.4 3D Model Generator

#### Purpose
Converts raw geometry into optimized, renderable 3D assets.

#### Responsibilities
- Mesh optimization
- UV unwrapping
- Texture mapping
- Lighting presets
- Material assignment
- Export to GLB / GLTF

#### Outputs
- Web-optimized 3D models
- VR-ready assets
- Scene graphs

---

## 6. AI / ML Pipeline

### Components

#### 1. Computer Vision Models
- Wall detection
- Door/window detection
- Symbol recognition
- Text extraction
- Room boundary segmentation

#### 2. LLM Integration (Claude / GPT)
- Intent parsing
- Constraint reasoning
- Semantic layout generation
- Style inference
- Design suggestions

---

## 7. Data Layer

### 7.1 PostgreSQL + PostGIS
Used for structured, relational, and spatial data.

#### Stores
- Users
- Roles
- Permissions
- Projects
- Spatial layouts
- Version history

#### Why
- ACID compliance
- Strong consistency
- Spatial queries
- Geometric operations

---

### 7.2 MongoDB
Used for flexible, evolving AI-generated data.

#### Stores
- NLP outputs
- CV model detections
- Layout schemas
- Configuration files
- AI experiment logs

---

### 7.3 Redis Cache

#### Used For
- Session storage
- Real-time collaboration state
- Temporary inference results
- WebSocket state

---

### 7.4 Object Storage (S3)

#### Used For
- Blueprint images
- Generated 3D models
- Textures
- Rendered previews
- Videos

---

## 8. Primary Data Flows

### 8.1 Blueprint to 3D Flow

User Uploads Blueprint  
→ Blueprint Processing Service  
→ Computer Vision Models  
→ 2D → 3D Engine  
→ 3D Model Generator  
→ 3D Viewer  

---

### 8.2 Text to 3D Flow

User Writes Description  
→ NLP Service  
→ LLM Integration  
→ 2D → 3D Engine  
→ 3D Model Generator  
→ 3D Viewer  

---

### 8.3 Hybrid Flow

Blueprint + Text Constraints  
→ Blueprint Processing + NLP  
→ Merged Layout Schema  
→ 2D → 3D Engine  
→ 3D Model Generator  
→ Interactive Walkthrough  

---

## 9. Architectural Benefits

- Horizontal scalability
- AI model replaceability
- Independent service deployment
- Real-time collaboration support
- Multi-input support (image + text)
- VR and Web compatibility
- Future extensibility

---

## 10. Future Enhancements

- GPU inference clusters
- Real-time ray tracing
- Procedural furniture generation
- Style transfer models
- BIM export support
- AR mode

---

## 11. Summary

This architecture enables a robust, scalable, and AI-driven 2D-to-3D conversion platform. It cleanly separates responsibilities across layers, supports real-time collaboration, and is optimized for future ML innovations.
