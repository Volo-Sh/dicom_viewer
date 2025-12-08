# dicom_viewer
CBCT Web Viewer

A browser-based application that allows users to upload, process, and view CBCT (Cone Beam Computed Tomography) images online for free.
The goal of this project is to create a simple, secure, and intuitive tool for viewing medical volumetric scans directly in the browser - without installing additional software.

Project Status - In Development (Portfolio Project)

Plan to do 12 steps 

**Stage 1 - Define Project Scope**
**Main goal:**
Provide users with a fully free, simple, fast, and accessible way to upload and view CBCT (Cone Beam Computed Tomography) scans directly in a web browser, without installing any specialized software.

**Target users:**
Dental and orthodontic professionals, radiology and medical students, patients, and developers or researchers working with medical imaging.

**Core use-case:**
User logs in → uploads a CBCT file → the system processes the scan → the scan appears in the dashboard → user opens it in the viewer → user scrolls through slices directly in the browser.

**Limitations:**
Supported formats: DICOM, NRRD, NII.
Max file size: approximately 200–400 MB.
Processing time: depends on scan size and browser performance; large files may load slowly.

**Stage 2 Choose Tech Stack and Define Architecture**

**Frontend stack:**
React + Vite + Three.js for building the interface and rendering volumetric CBCT data in the browser.

**Backend stack:**
Node.js + Express for handling authentication, file uploads, file processing, and providing API endpoints.

**Database:**
MongoDB for storing user accounts, scan metadata, and references to uploaded files.

**Storage approach:**
Local file storage for the initial version of the project, with the option to move to cloud storage in the future.

**Architecture:**
Frontend communicates with the backend through a REST API.
Data flow: the user uploads a CBCT scan → backend validates and stores the file → metadata is written to MongoDB → the frontend requests processed data → the scan is rendered in the viewer using React and Three.js.
