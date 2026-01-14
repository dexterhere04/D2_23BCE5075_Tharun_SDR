# 2D Blueprint to 3D Converter & Floor Plan Generator

Transform 2D architectural blueprints into interactive 3D models and 
generate precise 2D floor plans from natural language descriptions. This
 open-source project leverages computer vision, machine learning, and 
generative AI to streamline architectural workflows for designers, 
builders, and planners

## Core Features




Converts
 scanned or digital 2D blueprints (JPG, PNG, PDF) to detailed 3D models 
in formats like OBJ, GLTF, and FBX using edge detection, depth 
estimation, and extrusion algorithms.
​



## Tech Stack
Tech Stack


Backend:
 Python 3.8+, OpenCV for image processing, Mask R-CNN for object 
detection, Stable Diffusion or Depth-Anything for 3D reconstruction.
​




Floor Plan Generation: LangChain or Llama for text-to-layout, SVG/Canvas for 2D rendering.
​




Frontend: Gradio or Streamlit for UI, Three.js for 3D previews.




Dependencies: NumPy, PyTorch, Blender Python API;

Generates
 2D floor plans from text prompts  via NLP parsing and vector graphics rendering.
​






Supports texture mapping, wall height customization, and export to Blender or Unity for further editing.
​






Web-based demo for instant testing without installation.
​
