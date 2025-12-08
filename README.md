# dicom_viewer
CBCT Web Viewer

A browser-based application that allows users to upload, process, and view CBCT (Cone Beam Computed Tomography) images online for free.
The goal of this project is to create a simple, secure, and intuitive tool for viewing medical volumetric scans directly in the browser - without installing additional software.

Project Status - In Development (Portfolio Project)

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

**Stage 3 - Design UI/UX and User Flows**

**Landing page defined:**
Clear introduction of the service, buttons to log in or create an account, and a disclaimer stating that the service provides no medical advice or responsibility

**Login and registration pages defined:**
Login includes email, password, a Create account link and a placeholder for Google login.
Registration includes required fields and a sign-up button.

**User dashboard defined:**
Displays a list of uploaded CBCT studies with filename (from the doctor’s original file name) and upload date.
Includes buttons to upload new scans and delete existing ones.
Supports two statuses: ready and failed (unsupported or problematic files).
Scans can be opened directly in the viewer.

**CBCT viewer defined:**
Four-view layout: axial, sagittal, coronal and a 3D model window.
Slice navigation via slider or scroll.
Buttons for Back to dashboard and Reset view.
Zoom and pan planned for future.

**Profile/Settings page defined:**
Includes a basic change-password form.

**Main user flows defined:**
Registration flow, login flow, upload flow, scan viewing flow and error handling cases.

**Design direction established:**
Clean and minimal UI, simple color palette, consistent spacing and intuitive layout across all pages.

**Stage 4 - Define Data Model and API Structure**

**Core entities defined:**
**User**: id, email, password hash, createdAt
**CBCTScan**: id, ownerId, originalFileName, storagePath, uploadDate, status (ready, failed), format
**ScanMetadata**: scanId, dimensions, numberOfSlices, voxelSize (optional later)

**Database responsibilities defined:**
User data and scan metadata are stored in MongoDB.
Actual CBCT files are stored in filesystem (local storage first).
Metadata links each file to its user and storage path.

**API endpoints defined:**

Authentication:
POST /auth/register
POST /auth/login

Scan management:
POST /scans/upload
GET /scans/list
DELETE /scans/:scanId
GET /scans/:scanId/info

Viewer data:
GET /scans/:scanId/slices/:index (returns processed slice)
GET /scans/:scanId/3d (3D data placeholder for future)

**File validation and processing defined**:
Backend validates file type (DICOM, NRRD, NII).
If unsupported — scan is marked as failed.
Metadata is extracted during upload (dimensions, slices).
Processed data stored alongside original file.

**Storage structure defined**:
Files stored under /storage/userId/scanId/
Original file name preserved for display.
Processed slices stored as separate files (for future optimization).

**Security rules defined**:
Users can access only their own scans.
File upload sanitized and validated.
All endpoints require authentication except login and registration.
