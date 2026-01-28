
---
In Blender, **Shade Smooth** is a rendering property that creates the visual illusion of a curved surface without changing the actual geometry of a mesh.

###### **Key Takeaways:**
- How it works: Instead of rendering each face as a flat block (Shade Flat), it interpolates light across the faces by smoothing the "normals" between vertices.
- Visuals: It makes low-polygon objects look organic and rounded, though the silhouette (outer edge) will still appear jagged if the poly count is low.
- Geometry: It does not add more polygons or sub-divide the mesh; it only affects how light hits the surface.