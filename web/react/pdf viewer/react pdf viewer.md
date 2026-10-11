নিচে একটি **complete React + Tailwind PDF Viewer** দিলাম—toolbar, zoom, pagination, search এবং fullscreen সহ। `react-pdf` ব্যবহার করছি, যাতে PDF-এর text layer-ও থাকে।

 ### 1\. Install

```
npm install react-pdf pdfjs-dist lucide-react
```

 ### 2\. `PdfViewer.jsx`

 Modern React PDF Viewer

```
import { useEffect, useRef, useState } from "react";
import { Document, Page, pdfjs } from "react-pdf";
import {
  ChevronLeft,
  ChevronRight,
  Download,
  Maximize,
  Minimize,
  Minus,
  Plus,
  Search,
  X,
} from "lucide-react";

import "react-pdf/dist/Page/TextLayer.css";
import "react-pdf/dist/Page/AnnotationLayer.css";

pdfjs.GlobalWorkerOptions.workerSrc = new URL(
  "pdfjs-dist/build/pdf.worker.min.mjs",
  import.meta.url
).toString();

export default function PdfViewer({
  file = "/sample.pdf",
}) {
  const viewerRef = useRef(null);

  const [numPages, setNumPages] = useState(0);
  const [pageNumber, setPageNumber] = useState(1);
  const [scale, setScale] = useState(1);
  const [isFullscreen, setIsFullscreen] = useState(false);

  const [searchOpen, setSearchOpen] = useState(false);
  const [searchText, setSearchText] = useState("");

  const MIN_SCALE = 0.5;
  const MAX_SCALE = 2.5;
  const SCALE_STEP = 0.1;

  function onDocumentLoadSuccess({ numPages }) {
    setNumPages(numPages);
    setPageNumber(1);
  }

  function zoomIn() {
    setScale((current) =>
      Math.min(MAX_SCALE, +(current + SCALE_STEP).toFixed(2))
    );
  }

  function zoomOut() {
    setScale((current) =>
      Math.max(MIN_SCALE, +(current - SCALE_STEP).toFixed(2))
    );
  }

  function resetZoom() {
    setScale(1);
  }

  function previousPage() {
    setPageNumber((current) => Math.max(1, current - 1));
  }

  function nextPage() {
    setPageNumber((current) =>
      Math.min(numPages, current + 1)
    );
  }

  function goToPage(event) {
    const value = Number(event.target.value);

    if (!Number.isNaN(value)) {
      setPageNumber(
        Math.min(numPages, Math.max(1, value))
      );
    }
  }

  function toggleFullscreen() {
    if (!document.fullscreenElement) {
      viewerRef.current?.requestFullscreen();
    } else {
      document.exitFullscreen();
    }
  }

  useEffect(() => {
    function handleFullscreenChange() {
      setIsFullscreen(
        document.fullscreenElement === viewerRef.current
      );
    }

    document.addEventListener(
      "fullscreenchange",
      handleFullscreenChange
    );

    return () => {
      document.removeEventListener(
        "fullscreenchange",
        handleFullscreenChange
      );
    };
  }, []);

  function handleSearchKeyDown(event) {
    if (event.key === "Escape") {
      setSearchOpen(false);
      setSearchText("");
    }
  }

  return (
    <div
      ref={viewerRef}
      className="flex h-screen w-full flex-col overflow-hidden bg-slate-100 text-slate-900"
    >
      {/* Toolbar */}
      <header className="z-50 flex h-14 shrink-0 items-center justify-between border-b border-slate-200 bg-white px-3 shadow-sm">
        {/* Left */}
        <div className="flex min-w-0 items-center gap-2">
          <div className="flex h-9 w-9 shrink-0 items-center justify-center rounded-lg bg-red-500 text-sm font-bold text-white">
            PDF
          </div>

          <div className="hidden min-w-0 sm:block">
            <p className="truncate text-sm font-semibold">
              Document.pdf
            </p>
            <p className="text-xs text-slate-500">
              PDF Document
            </p>
          </div>
        </div>

        {/* Center controls */}
        <div className="absolute left-1/2 flex -translate-x-1/2 items-center gap-1">
          {/* Previous */}
          <ToolbarButton
            onClick={previousPage}
            disabled={pageNumber <= 1}
            title="Previous page"
          >
            <ChevronLeft size={18} />
          </ToolbarButton>

          {/* Page input */}
          <div className="flex h-9 items-center gap-1 rounded-lg border border-slate-200 bg-slate-50 px-2">
            <input
              value={pageNumber}
              onChange={goToPage}
              className="w-8 bg-transparent text-center text-sm outline-none"
              min={1}
              max={numPages}
              type="number"
            />

            <span className="text-sm text-slate-400">
              /
            </span>

            <span className="min-w-5 text-sm text-slate-600">
              {numPages || "-"}
            </span>
          </div>

          {/* Next */}
          <ToolbarButton
            onClick={nextPage}
            disabled={
              !numPages || pageNumber >= numPages
            }
            title="Next page"
          >
            <ChevronRight size={18} />
          </ToolbarButton>
        </div>

        {/* Right */}
        <div className="flex items-center gap-1">
          {/* Search */}
          <ToolbarButton
            onClick={() => setSearchOpen((value) => !value)}
            title="Search"
          >
            <Search size={18} />
          </ToolbarButton>

          {/* Zoom */}
          <div className="hidden items-center rounded-lg border border-slate-200 bg-slate-50 md:flex">
            <ToolbarButton
              onClick={zoomOut}
              disabled={scale <= MIN_SCALE}
              title="Zoom out"
              border={false}
            >
              <Minus size={16} />
            </ToolbarButton>

            <button
              onClick={resetZoom}
              className="min-w-14 px-2 text-xs font-medium text-slate-600 hover:text-slate-900"
            >
              {Math.round(scale * 100)}%
            </button>

            <ToolbarButton
              onClick={zoomIn}
              disabled={scale >= MAX_SCALE}
              title="Zoom in"
              border={false}
            >
              <Plus size={16} />
            </ToolbarButton>
          </div>

          {/* Download */}
          <a
            href={file}
            download
            className="hidden h-9 w-9 items-center justify-center rounded-lg text-slate-600 transition hover:bg-slate-100 hover:text-slate-900 sm:flex"
            title="Download"
          >
            <Download size={18} />
          </a>

          {/* Fullscreen */}
          <ToolbarButton
            onClick={toggleFullscreen}
            title={
              isFullscreen
                ? "Exit fullscreen"
                : "Fullscreen"
            }
          >
            {isFullscreen ? (
              <Minimize size={18} />
            ) : (
              <Maximize size={18} />
            )}
          </ToolbarButton>
        </div>
      </header>

      {/* Search bar */}
      {searchOpen && (
        <div className="z-40 flex h-12 items-center justify-center border-b border-slate-200 bg-white px-4 shadow-sm">
          <div className="flex w-full max-w-lg items-center rounded-lg border border-slate-300 bg-slate-50 px-3">
            <Search
              size={17}
              className="shrink-0 text-slate-400"
            />

            <input
              autoFocus
              value={searchText}
              onChange={(e) =>
                setSearchText(e.target.value)
              }
              onKeyDown={handleSearchKeyDown}
              placeholder="Search in PDF..."
              className="h-9 w-full bg-transparent px-2 text-sm outline-none"
            />

            {searchText && (
              <button
                onClick={() => setSearchText("")}
                className="rounded p-1 text-slate-400 hover:bg-slate-200 hover:text-slate-700"
              >
                <X size={16} />
              </button>
            )}
          </div>
        </div>
      )}

      {/* PDF Area */}
      <main className="flex-1 overflow-auto bg-slate-200">
        <div className="flex min-h-full justify-center p-4 sm:p-8">
          <Document
            file={file}
            onLoadSuccess={onDocumentLoadSuccess}
            loading={
              <LoadingState text="Loading PDF..." />
            }
            error={
              <ErrorState />
            }
          >
            {numPages > 0 && (
              <div className="flex justify-center">
                <div className="overflow-hidden rounded-sm bg-white shadow-xl">
                  <Page
                    pageNumber={pageNumber}
                    scale={scale}
                    renderTextLayer
                    renderAnnotationLayer
                  />
                </div>
              </div>
            )}
          </Document>
        </div>
      </main>

      {/* Mobile bottom toolbar */}
      <div className="flex h-12 shrink-0 items-center justify-center gap-3 border-t border-slate-200 bg-white md:hidden">
        <ToolbarButton
          onClick={zoomOut}
          disabled={scale <= MIN_SCALE}
        >
          <Minus size={17} />
        </ToolbarButton>

        <button
          onClick={resetZoom}
          className="min-w-12 text-xs font-medium"
        >
          {Math.round(scale * 100)}%
        </button>

        <ToolbarButton
          onClick={zoomIn}
          disabled={scale >= MAX_SCALE}
        >
          <Plus size={17} />
        </ToolbarButton>
      </div>
    </div>
  );
}

/* -------------------------------- */
/* Reusable toolbar button */
/* -------------------------------- */

function ToolbarButton({
  children,
  onClick,
  disabled = false,
  title,
  border = true,
}) {
  return (
    <button
      onClick={onClick}
      disabled={disabled}
      title={title}
      className={[
        "flex h-9 w-9 items-center justify-center rounded-lg",
        "text-slate-600 transition",
        "hover:bg-slate-100 hover:text-slate-900",
        "disabled:cursor-not-allowed disabled:opacity-30",
        border
          ? "border border-transparent"
          : "",
      ].join(" ")}
    >
      {children}
    </button>
  );
}

/* -------------------------------- */
/* Loading */
/* -------------------------------- */

function LoadingState({ text }) {
  return (
    <div className="flex min-h-[400px] min-w-[300px] items-center justify-center">
      <div className="text-center">
        <div className="mx-auto mb-3 h-8 w-8 animate-spin rounded-full border-4 border-slate-300 border-t-blue-500" />
        <p className="text-sm text-slate-500">
          {text}
        </p>
      </div>
    </div>
  );
}

/* -------------------------------- */
/* Error */
/* -------------------------------- */

function ErrorState() {
  return (
    <div className="flex min-h-[400px] items-center justify-center">
      <div className="text-center">
        <div className="mb-3 text-4xl">📄</div>

        <h3 className="font-semibold text-slate-800">
          Failed to load PDF
        </h3>

        <p className="mt-1 text-sm text-slate-500">
          Please check the PDF file or URL.
        </p>
      </div>
    </div>
  );
}
```

 ### 3\. Use it

```
import PdfViewer from "./PdfViewer";

export default function App() {
  return <PdfViewer file="/sample.pdf" />;
}
```

 `sample.pdf` রাখুন:

```
your-project/
├── public/
│   └── sample.pdf
├── src/
│   ├── App.jsx
│   └── PdfViewer.jsx
├── package.json
└── ...
```

 ## গুরুত্বপূর্ণ: Search

 উপরের `Search` UI তৈরি করা হয়েছে, কিন্তু **বাস্তবে PDF-এর text search করার logic এখনো যোগ করা হয়নি**। `react-pdf` text layer render করে, কিন্তু search-এর জন্য PDF-এর text content বের করে matching page/word highlight করার logic আলাদাভাবে করতে হয়।

 আপনি যদি **Acrobat-এর মতো real search** চান, তাহলে architecture-টা এমন করা ভালো:

```
PDF
 │
 ├── Toolbar
 │    ├── Search
 │    ├── Zoom
 │    ├── Download
 │    └── Fullscreen
 │
 ├── Page Navigation
 │
 └── PDF Canvas
      ├── PDF Layer
      ├── Text Layer
      └── Annotation Layer
```

 আর production-level viewer হলে আমি `Search + text highlight + keyboard shortcuts (Ctrl/Cmd+F, ←/→, +/−) + continuous scrolling + page thumbnails + responsive mobile toolbar` একসাথে করার পরামর্শ দেব।



---
অবশ্যই। নিচেরটা **full reusable React \+ Tailwind PDF Viewer component**—backend API থেকে PDF dynamically load করবে এবং এতে থাকবে:

 - Dynamic backend PDF loading
- JWT/Bearer authentication support
- Previous/Next page
- Page number input
- Zoom in/out/reset
- Search UI
- Fullscreen
- Download
- Loading/error state
- Responsive toolbar
- Blob URL cleanup

 ধরে নিচ্ছি backend endpoint `GET /api/documents/:id/pdf` এবং Bearer token ব্যবহার করছে।

```
import {
  useCallback,
  useEffect,
  useRef,
  useState,
} from "react";

import {
  ChevronLeft,
  ChevronRight,
  Download,
  FileText,
  Maximize,
  Minimize,
  Minus,
  Plus,
  RotateCcw,
  Search,
  X,
} from "lucide-react";

import {
  Document,
  Page,
  pdfjs,
} from "react-pdf";

import "react-pdf/dist/Page/TextLayer.css";
import "react-pdf/dist/Page/AnnotationLayer.css";

/*
|--------------------------------------------------------------------------
| PDF.js Worker
|--------------------------------------------------------------------------
*/

pdfjs.GlobalWorkerOptions.workerSrc = new URL(
  "pdfjs-dist/build/pdf.worker.min.mjs",
  import.meta.url
).toString();

/*
|--------------------------------------------------------------------------
| Main Component
|--------------------------------------------------------------------------
*/

export default function PdfViewer({
  documentId,
  token,

  /*
   * Example:
   * http://localhost:5000/api/documents
   */
  apiBaseUrl = "http://localhost:5000/api/documents",

  /*
   * Optional custom PDF URL.
   *
   * If provided, documentId is ignored.
   */
  pdfUrl = null,

  className = "",
}) {
  const viewerRef = useRef(null);

  const [pdfFile, setPdfFile] = useState(null);

  const [loading, setLoading] = useState(true);
  const [error, setError] = useState("");

  const [numPages, setNumPages] = useState(0);
  const [pageNumber, setPageNumber] = useState(1);

  const [scale, setScale] = useState(1);

  const [isFullscreen, setIsFullscreen] =
    useState(false);

  const [searchOpen, setSearchOpen] =
    useState(false);

  const [searchText, setSearchText] =
    useState("");

  const MIN_SCALE = 0.5;
  const MAX_SCALE = 2.5;
  const SCALE_STEP = 0.1;

  /*
  |--------------------------------------------------------------------------
  | Load PDF from backend
  |--------------------------------------------------------------------------
  */

  const loadPdf = useCallback(async () => {
    let objectUrl = null;

    try {
      setLoading(true);
      setError("");

      /*
       * If custom URL is provided
       */
      if (pdfUrl) {
        setPdfFile(pdfUrl);
        setLoading(false);
        return;
      }

      if (!documentId) {
        throw new Error("Document ID is required");
      }

      const url =
        `${apiBaseUrl}/${documentId}/pdf`;

      const headers = {};

      if (token) {
        headers.Authorization =
          `Bearer ${token}`;
      }

      const response = await fetch(url, {
        method: "GET",
        headers,
      });

      if (!response.ok) {
        throw new Error(
          `Failed to load PDF (${response.status})`
        );
      }

      const contentType =
        response.headers.get("content-type");

      if (
        contentType &&
        !contentType.includes("application/pdf")
      ) {
        throw new Error(
          "Server did not return a PDF file."
        );
      }

      const blob = await response.blob();

      objectUrl = URL.createObjectURL(blob);

      setPdfFile(objectUrl);
    } catch (err) {
      console.error(err);

      setError(
        err?.message ||
          "Failed to load PDF."
      );
    } finally {
      setLoading(false);
    }

    return objectUrl;
  }, [
    documentId,
    token,
    apiBaseUrl,
    pdfUrl,
  ]);

  /*
  |--------------------------------------------------------------------------
  | Fetch PDF
  |--------------------------------------------------------------------------
  */

  useEffect(() => {
    let currentObjectUrl = null;

    async function fetchPdf() {
      const url = await loadPdf();

      if (url?.startsWith("blob:")) {
        currentObjectUrl = url;
      }
    }

    fetchPdf();

    return () => {
      if (currentObjectUrl) {
        URL.revokeObjectURL(
          currentObjectUrl
        );
      }
    };
  }, [loadPdf]);

  /*
  |--------------------------------------------------------------------------
  | PDF loaded
  |--------------------------------------------------------------------------
  */

  function handleDocumentLoadSuccess({
    numPages,
  }) {
    setNumPages(numPages);
    setPageNumber(1);
    setLoading(false);
  }

  /*
  |--------------------------------------------------------------------------
  | Page navigation
  |--------------------------------------------------------------------------
  */

  function previousPage() {
    setPageNumber((current) =>
      Math.max(1, current - 1)
    );
  }

  function nextPage() {
    setPageNumber((current) =>
      Math.min(
        numPages,
        current + 1
      )
    );
  }

  function handlePageChange(event) {
    let value = Number(
      event.target.value
    );

    if (Number.isNaN(value)) {
      return;
    }

    value = Math.max(
      1,
      Math.min(numPages, value)
    );

    setPageNumber(value);
  }

  /*
  |--------------------------------------------------------------------------
  | Zoom
  |--------------------------------------------------------------------------
  */

  function zoomIn() {
    setScale((current) =>
      Math.min(
        MAX_SCALE,
        +(current + SCALE_STEP).toFixed(2)
      )
    );
  }

  function zoomOut() {
    setScale((current) =>
      Math.max(
        MIN_SCALE,
        +(current - SCALE_STEP).toFixed(2)
      )
    );
  }

  function resetZoom() {
    setScale(1);
  }

  /*
  |--------------------------------------------------------------------------
  | Fullscreen
  |--------------------------------------------------------------------------
  */

  function toggleFullscreen() {
    if (!document.fullscreenElement) {
      viewerRef.current?.requestFullscreen();
    } else {
      document.exitFullscreen();
    }
  }

  useEffect(() => {
    function handleFullscreenChange() {
      setIsFullscreen(
        document.fullscreenElement ===
          viewerRef.current
      );
    }

    document.addEventListener(
      "fullscreenchange",
      handleFullscreenChange
    );

    return () => {
      document.removeEventListener(
        "fullscreenchange",
        handleFullscreenChange
      );
    };
  }, []);

  /*
  |--------------------------------------------------------------------------
  | Keyboard shortcuts
  |--------------------------------------------------------------------------
  */

  useEffect(() => {
    function handleKeyboard(event) {
      /*
       * Don't trigger shortcuts while typing
       */
      const tag =
        event.target?.tagName;

      if (
        tag === "INPUT" ||
        tag === "TEXTAREA"
      ) {
        return;
      }

      if (event.key === "ArrowLeft") {
        previousPage();
      }

      if (event.key === "ArrowRight") {
        nextPage();
      }

      if (
        event.key === "+" ||
        event.key === "="
      ) {
        zoomIn();
      }

      if (event.key === "-") {
        zoomOut();
      }

      if (event.key === "0") {
        resetZoom();
      }

      if (
        (event.ctrlKey ||
          event.metaKey) &&
        event.key.toLowerCase() ===
          "f"
      ) {
        event.preventDefault();

        setSearchOpen(true);
      }

      if (event.key === "Escape") {
        setSearchOpen(false);
      }
    }

    window.addEventListener(
      "keydown",
      handleKeyboard
    );

    return () => {
      window.removeEventListener(
        "keydown",
        handleKeyboard
      );
    };
  }, [numPages]);

  /*
  |--------------------------------------------------------------------------
  | Render
  |--------------------------------------------------------------------------
  */

  return (
    <div
      ref={viewerRef}
      className={[
        "flex h-screen w-full flex-col",
        "overflow-hidden bg-slate-100",
        className,
      ].join(" ")}
    >
      {/* ========================================================= */}
      {/* TOOLBAR */}
      {/* ========================================================= */}

      <header
        className="
          z-50 flex h-14 shrink-0
          items-center justify-between
          border-b border-slate-200
          bg-white px-3 shadow-sm
        "
      >
        {/* ----------------------------------------------------- */}
        {/* LEFT */}
        {/* ----------------------------------------------------- */}

        <div className="flex min-w-0 items-center gap-3">
          <div
            className="
              flex h-9 w-9 shrink-0
              items-center justify-center
              rounded-lg bg-red-500
              text-xs font-bold text-white
            "
          >
            PDF
          </div>

          <div className="hidden min-w-0 sm:block">
            <p className="truncate text-sm font-semibold text-slate-800">
              PDF Document
            </p>

            <p className="text-xs text-slate-400">
              {numPages
                ? `${numPages} pages`
                : "Loading..."}
            </p>
          </div>
        </div>

        {/* ----------------------------------------------------- */}
        {/* CENTER */}
        {/* ----------------------------------------------------- */}

        <div
          className="
            absolute left-1/2
            flex -translate-x-1/2
            items-center gap-1
          "
        >
          <IconButton
            onClick={previousPage}
            disabled={pageNumber <= 1}
            title="Previous page"
          >
            <ChevronLeft size={18} />
          </IconButton>

          {/* PAGE INPUT */}

          <div
            className="
              flex h-9 items-center
              rounded-lg border
              border-slate-200
              bg-slate-50 px-2
            "
          >
            <input
              type="number"
              value={pageNumber}
              min={1}
              max={numPages || 1}
              onChange={handlePageChange}
              className="
                w-9 bg-transparent
                text-center text-sm
                font-medium outline-none
              "
            />

            <span className="px-1 text-sm text-slate-400">
              /
            </span>

            <span className="min-w-5 text-sm text-slate-600">
              {numPages || "-"}
            </span>
          </div>

          <IconButton
            onClick={nextPage}
            disabled={
              !numPages ||
              pageNumber >= numPages
            }
            title="Next page"
          >
            <ChevronRight size={18} />
          </IconButton>
        </div>

        {/* ----------------------------------------------------- */}
        {/* RIGHT */}
        {/* ----------------------------------------------------- */}

        <div className="flex items-center gap-1">
          {/* SEARCH */}

          <IconButton
            onClick={() =>
              setSearchOpen(
                (current) => !current
              )
            }
            title="Search"
          >
            <Search size={18} />
          </IconButton>

          {/* ZOOM */}

          <div
            className="
              hidden items-center
              rounded-lg border
              border-slate-200
              bg-slate-50 md:flex
            "
          >
            <IconButton
              onClick={zoomOut}
              disabled={
                scale <= MIN_SCALE
              }
              title="Zoom out"
              border={false}
            >
              <Minus size={16} />
            </IconButton>

            <button
              onClick={resetZoom}
              className="
                min-w-14 px-2
                text-xs font-medium
                text-slate-600
                hover:text-slate-900
              "
            >
              {Math.round(
                scale * 100
              )}
              %
            </button>

            <IconButton
              onClick={zoomIn}
              disabled={
                scale >= MAX_SCALE
              }
              title="Zoom in"
              border={false}
            >
              <Plus size={16} />
            </IconButton>
          </div>

          {/* DOWNLOAD */}

          <button
            onClick={() => {
              if (!pdfFile) return;

              const link =
                document.createElement(
                  "a"
                );

              link.href = pdfFile;
              link.download =
                "document.pdf";

              document.body.appendChild(
                link
              );

              link.click();

              link.remove();
            }}
            disabled={!pdfFile}
            className="
              hidden h-9 w-9
              items-center justify-center
              rounded-lg text-slate-600
              transition
              hover:bg-slate-100
              hover:text-slate-900
              disabled:opacity-30
              sm:flex
            "
            title="Download"
          >
            <Download size={18} />
          </button>

          {/* FULLSCREEN */}

          <IconButton
            onClick={toggleFullscreen}
            title={
              isFullscreen
                ? "Exit fullscreen"
                : "Fullscreen"
            }
          >
            {isFullscreen ? (
              <Minimize size={18} />
            ) : (
              <Maximize size={18} />
            )}
          </IconButton>
        </div>
      </header>

      {/* ========================================================= */}
      {/* SEARCH BAR */}
      {/* ========================================================= */}

      {searchOpen && (
        <div
          className="
            z-40 flex h-12
            items-center justify-center
            border-b border-slate-200
            bg-white px-4 shadow-sm
          "
        >
          <div
            className="
              flex w-full max-w-lg
              items-center
              rounded-lg border
              border-slate-300
              bg-slate-50 px-3
            "
          >
            <Search
              size={17}
              className="shrink-0 text-slate-400"
            />

            <input
              autoFocus
              value={searchText}
              onChange={(event) =>
                setSearchText(
                  event.target.value
                )
              }
              placeholder="Search in PDF..."
              className="
                h-9 w-full
                bg-transparent
                px-2 text-sm
                outline-none
              "
            />

            {searchText && (
              <button
                onClick={() =>
                  setSearchText("")
                }
                className="
                  rounded p-1
                  text-slate-400
                  hover:bg-slate-200
                "
              >
                <X size={16} />
              </button>
            )}
          </div>
        </div>
      )}

      {/* ========================================================= */}
      {/* PDF VIEWER */}
      {/* ========================================================= */}

      <main
        className="
          relative flex-1
          overflow-auto
          bg-slate-200
        "
      >
        {/* LOADING */}

        {loading && (
          <Loading />
        )}

        {/* ERROR */}

        {!loading && error && (
          <ErrorView
            error={error}
            onRetry={loadPdf}
          />
        )}

        {/* PDF */}

        {!error && pdfFile && (
          <div
            className="
              flex min-h-full
              justify-center
              p-4 sm:p-8
            "
          >
            <Document
              file={pdfFile}
              onLoadSuccess={
                handleDocumentLoadSuccess
              }
              loading={null}
              error={null}
            >
              <div
                className="
                  overflow-hidden
                  rounded-sm bg-white
                  shadow-2xl
                "
              >
                <Page
                  pageNumber={pageNumber}
                  scale={scale}
                  renderTextLayer
                  renderAnnotationLayer
                />
              </div>
            </Document>
          </div>
        )}
      </main>

      {/* ========================================================= */}
      {/* MOBILE BOTTOM BAR */}
      {/* ========================================================= */}

      <div
        className="
          flex h-12 shrink-0
          items-center justify-center
          gap-3 border-t
          border-slate-200
          bg-white md:hidden
        "
      >
        <IconButton
          onClick={zoomOut}
          disabled={scale <= MIN_SCALE}
        >
          <Minus size={17} />
        </IconButton>

        <button
          onClick={resetZoom}
          className="
            min-w-12 text-xs
            font-medium text-slate-600
          "
        >
          {Math.round(scale * 100)}%
        </button>

        <IconButton
          onClick={zoomIn}
          disabled={scale >= MAX_SCALE}
        >
          <Plus size={17} />
        </IconButton>
      </div>
    </div>
  );
}

/*
|--------------------------------------------------------------------------
| Icon Button
|--------------------------------------------------------------------------
*/

function IconButton({
  children,
  onClick,
  disabled = false,
  title,
  border = true,
}) {
  return (
    <button
      type="button"
      onClick={onClick}
      disabled={disabled}
      title={title}
      className={[
        "flex h-9 w-9",
        "items-center justify-center",
        "rounded-lg",
        "text-slate-600",
        "transition",
        "hover:bg-slate-100",
        "hover:text-slate-900",
        "disabled:cursor-not-allowed",
        "disabled:opacity-30",
        border
          ? "border border-transparent"
          : "",
      ].join(" ")}
    >
      {children}
    </button>
  );
}

/*
|--------------------------------------------------------------------------
| Loading
|--------------------------------------------------------------------------
*/

function Loading() {
  return (
    <div
      className="
        flex h-full
        min-h-[400px]
        items-center justify-center
      "
    >
      <div className="text-center">
        <div
          className="
            mx-auto mb-4
            h-10 w-10
            animate-spin
            rounded-full
            border-4
            border-slate-300
            border-t-blue-500
          "
        />

        <p className="text-sm text-slate-500">
          Loading PDF...
        </p>
      </div>
    </div>
  );
}

/*
|--------------------------------------------------------------------------
| Error
|--------------------------------------------------------------------------
*/

function ErrorView({
  error,
  onRetry,
}) {
  return (
    <div
      className="
        flex h-full
        min-h-[400px]
        items-center
        justify-center
        p-6
      "
    >
      <div
        className="
          max-w-sm
          text-center
        "
      >
        <div
          className="
            mx-auto mb-4
            flex h-14 w-14
            items-center justify-center
            rounded-full
            bg-red-100
            text-red-500
          "
        >
          <FileText size={26} />
        </div>

        <h3
          className="
            text-base
            font-semibold
            text-slate-800
          "
        >
          Unable to load PDF
        </h3>

        <p
          className="
            mt-2 text-sm
            text-slate-500
          "
        >
          {error}
        </p>

        <button
          onClick={onRetry}
          className="
            mt-5 inline-flex
            items-center gap-2
            rounded-lg
            bg-slate-900
            px-4 py-2
            text-sm font-medium
            text-white
            transition
            hover:bg-slate-700
          "
        >
          <RotateCcw size={15} />
          Try again
        </button>
      </div>
    </div>
  );
}
```

 ### ব্যবহার

 ধরুন backend:

```
GET http://localhost:5000/api/documents/123/pdf
```

 তাহলে:

```
import PdfViewer from "./components/PdfViewer";

export default function App() {
  const token = localStorage.getItem("access_token");

  return (
    <PdfViewer
      documentId="123"
      token={token}
      apiBaseUrl="http://localhost:5000/api/documents"
    />
  );
}
```

 তাহলে component নিজে থেকে call করবে:

```
GET /api/documents/123/pdf
Authorization: Bearer YOUR_TOKEN
```

 এবং response-এর PDF-কে `Blob → Object URL → react-pdf` দিয়ে render করবে।

 ### Backend response

 Backend-এ ideally এই headers থাকবে:

```
Content-Type: application/pdf
Content-Disposition: inline
```

 Express example:

```
app.get(
  "/api/documents/:id/pdf",
  authMiddleware,
  async (req, res) => {
    const document = await Document.findById(
      req.params.id
    );

    if (!document) {
      return res
        .status(404)
        .json({
          message: "Document not found",
        });
    }

    res.setHeader(
      "Content-Type",
      "application/pdf"
    );

    res.setHeader(
      "Content-Disposition",
      "inline"
    );

    res.sendFile(
      document.filePath
    );
  }
);
```

 **একটা গুরুত্বপূর্ণ বিষয়:** এই component-এর `Search` bar UI আছে, কিন্তু `react-pdf` নিজে Acrobat-এর মতো full-document search/highlight API দেয় না। তাই যদি আপনার requirement হয় **search করলে matching text highlight হবে + result count দেখাবে + Enter/Shift+Enter দিয়ে next/previous match হবে**, তাহলে search-এর জন্য আলাদা text-content extraction layer যোগ করতে হবে।
হ্যাঁ। `react-pdf` দিয়ে **real PDF search \+ highlight** করা যায়। সবচেয়ে practical approach হলো PDF.js-এর `getTextContent()` দিয়ে সব page-এর text index করা, তারপর `customTextRenderer` দিয়ে matching text highlight করা।

 নিচের component-এ থাকবে:

 - 🔎 পুরো PDF search
- 🟡 Matching text highlight
- `Enter` → next match
- `Shift + Enter` → previous match
- `↑ ↓` buttons
- `3 / 27 matches` counter
- Match পাওয়া page-এ automatically jump
- Backend থেকে dynamic PDF
- JWT authentication
- Zoom
- Pagination
- Fullscreen
- Download

 ## Complete component

```
import {
  useCallback,
  useEffect,
  useRef,
  useState,
} from "react";

import {
  ChevronLeft,
  ChevronRight,
  ChevronUp,
  ChevronDown,
  Download,
  FileText,
  Maximize,
  Minimize,
  Minus,
  Plus,
  RotateCcw,
  Search,
  X,
} from "lucide-react";

import {
  Document,
  Page,
  pdfjs,
} from "react-pdf";

import "react-pdf/dist/Page/TextLayer.css";
import "react-pdf/dist/Page/AnnotationLayer.css";

pdfjs.GlobalWorkerOptions.workerSrc = new URL(
  "pdfjs-dist/build/pdf.worker.min.mjs",
  import.meta.url
).toString();

export default function PdfViewer({
  documentId,
  token,
  apiBaseUrl = "http://localhost:5000/api/documents",
  pdfUrl = null,
}) {
  const viewerRef = useRef(null);
  const searchInputRef = useRef(null);

  const [pdfFile, setPdfFile] = useState(null);
  const [pdfDocument, setPdfDocument] = useState(null);

  const [loading, setLoading] = useState(true);
  const [error, setError] = useState("");

  const [numPages, setNumPages] = useState(0);
  const [pageNumber, setPageNumber] = useState(1);

  const [scale, setScale] = useState(1);

  const [isFullscreen, setIsFullscreen] =
    useState(false);

  /*
   * Search state
   */
  const [searchOpen, setSearchOpen] =
    useState(false);

  const [searchText, setSearchText] =
    useState("");

  const [searchResults, setSearchResults] =
    useState([]);

  const [currentMatch, setCurrentMatch] =
    useState(0);

  /*
   * Text cache:
   *
   * {
   *   1: "text from page 1...",
   *   2: "text from page 2...",
   * }
   */
  const textCache = useRef({});

  const MIN_SCALE = 0.5;
  const MAX_SCALE = 2.5;
  const SCALE_STEP = 0.1;

  /*
  |--------------------------------------------------------------------------
  | Load PDF
  |--------------------------------------------------------------------------
  */

  const loadPdf = useCallback(async () => {
    let objectUrl = null;

    try {
      setLoading(true);
      setError("");

      /*
       * Direct URL
       */
      if (pdfUrl) {
        setPdfFile(pdfUrl);
        setLoading(false);

        return pdfUrl;
      }

      if (!documentId) {
        throw new Error(
          "Document ID is required"
        );
      }

      const url =
        `${apiBaseUrl}/${documentId}/pdf`;

      const headers = {};

      if (token) {
        headers.Authorization =
          `Bearer ${token}`;
      }

      const response = await fetch(url, {
        method: "GET",
        headers,
      });

      if (!response.ok) {
        throw new Error(
          `Failed to load PDF (${response.status})`
        );
      }

      const contentType =
        response.headers.get(
          "content-type"
        );

      if (
        contentType &&
        !contentType.includes(
          "application/pdf"
        )
      ) {
        throw new Error(
          "Server did not return a PDF."
        );
      }

      const blob =
        await response.blob();

      objectUrl =
        URL.createObjectURL(blob);

      setPdfFile(objectUrl);

      return objectUrl;
    } catch (err) {
      console.error(err);

      setError(
        err?.message ||
          "Failed to load PDF."
      );

      return null;
    } finally {
      setLoading(false);
    }
  }, [
    documentId,
    token,
    apiBaseUrl,
    pdfUrl,
  ]);

  /*
  |--------------------------------------------------------------------------
  | Initial PDF load
  |--------------------------------------------------------------------------
  */

  useEffect(() => {
    let objectUrl = null;

    async function fetchPdf() {
      const result =
        await loadPdf();

      if (
        result?.startsWith("blob:")
      ) {
        objectUrl = result;
      }
    }

    fetchPdf();

    return () => {
      if (objectUrl) {
        URL.revokeObjectURL(
          objectUrl
        );
      }
    };
  }, [loadPdf]);

  /*
  |--------------------------------------------------------------------------
  | PDF loaded
  |--------------------------------------------------------------------------
  */

  async function handleDocumentLoadSuccess(
    pdf
  ) {
    setPdfDocument(pdf);
    setNumPages(pdf.numPages);
    setPageNumber(1);

    /*
     * Reset search cache
     */
    textCache.current = {};
    setSearchResults([]);
    setCurrentMatch(0);

    /*
     * Preload text content.
     *
     * For very large PDFs, you may want
     * to do this lazily instead.
     */
    try {
      for (
        let page = 1;
        page <= pdf.numPages;
        page++
      ) {
        const pdfPage =
          await pdf.getPage(page);

        const content =
          await pdfPage.getTextContent();

        const text =
          content.items
            .map((item) =>
              item.str || ""
            )
            .join(" ");

        textCache.current[page] =
          text;
      }
    } catch (err) {
      console.error(
        "Failed to index PDF text:",
        err
      );
    }
  }

  /*
  |--------------------------------------------------------------------------
  | Search PDF
  |--------------------------------------------------------------------------
  */

  useEffect(() => {
    if (!searchText.trim()) {
      setSearchResults([]);
      setCurrentMatch(0);
      return;
    }

    const query =
      searchText
        .trim()
        .toLowerCase();

    const results = [];

    for (
      let page = 1;
      page <= numPages;
      page++
    ) {
      const text =
        textCache.current[page];

      if (!text) continue;

      const lowerText =
        text.toLowerCase();

      let start = 0;

      while (true) {
        const index =
          lowerText.indexOf(
            query,
            start
          );

        if (index === -1) break;

        results.push({
          page,
          index,
        });

        start =
          index + query.length;
      }
    }

    setSearchResults(results);
    setCurrentMatch(
      results.length > 0 ? 1 : 0
    );

    /*
     * Jump to first result
     */
    if (results.length > 0) {
      setPageNumber(
        results[0].page
      );
    }
  }, [
    searchText,
    numPages,
  ]);

  /*
  |--------------------------------------------------------------------------
  | Navigate search results
  |--------------------------------------------------------------------------
  */

  function goToNextMatch() {
    if (!searchResults.length) {
      return;
    }

    const next =
      currentMatch >=
      searchResults.length
        ? 1
        : currentMatch + 1;

    setCurrentMatch(next);

    const result =
      searchResults[next - 1];

    setPageNumber(result.page);
  }

  function goToPreviousMatch() {
    if (!searchResults.length) {
      return;
    }

    const previous =
      currentMatch <= 1
        ? searchResults.length
        : currentMatch - 1;

    setCurrentMatch(previous);

    const result =
      searchResults[previous - 1];

    setPageNumber(result.page);
  }

  /*
  |--------------------------------------------------------------------------
  | Highlight text
  |--------------------------------------------------------------------------
  */

  function highlightText(
    text
  ) {
    if (
      !searchText.trim() ||
      !text
    ) {
      return text;
    }

    const query =
      searchText.trim();

    /*
     * Escape regex characters
     */
    const escaped =
      query.replace(
        /[.*+?^${}()|[\]\\]/g,
        "\\$&"
      );

    const regex =
      new RegExp(
        `(${escaped})`,
        "gi"
      );

    const parts =
      text.split(regex);

    return parts.map(
      (part, index) => {
        const isMatch =
          part.toLowerCase() ===
          query.toLowerCase();

        if (isMatch) {
          return (
            <mark
              key={index}
              className="
                rounded-sm
                bg-yellow-300
                px-[1px]
                text-black
              "
            >
              {part}
            </mark>
          );
        }

        return (
          <span key={index}>
            {part}
          </span>
        );
      }
    );
  }

  /*
  |--------------------------------------------------------------------------
  | Page navigation
  |--------------------------------------------------------------------------
  */

  function previousPage() {
    setPageNumber((current) =>
      Math.max(1, current - 1)
    );
  }

  function nextPage() {
    setPageNumber((current) =>
      Math.min(
        numPages,
        current + 1
      )
    );
  }

  function handlePageChange(
    event
  ) {
    const value =
      Number(event.target.value);

    if (
      Number.isNaN(value)
    ) {
      return;
    }

    setPageNumber(
      Math.max(
        1,
        Math.min(
          numPages,
          value
        )
      )
    );
  }

  /*
  |--------------------------------------------------------------------------
  | Zoom
  |--------------------------------------------------------------------------
  */

  function zoomIn() {
    setScale((current) =>
      Math.min(
        MAX_SCALE,
        +(current + SCALE_STEP)
          .toFixed(2)
      )
    );
  }

  function zoomOut() {
    setScale((current) =>
      Math.max(
        MIN_SCALE,
        +(current - SCALE_STEP)
          .toFixed(2)
      )
    );
  }

  function resetZoom() {
    setScale(1);
  }

  /*
  |--------------------------------------------------------------------------
  | Fullscreen
  |--------------------------------------------------------------------------
  */

  function toggleFullscreen() {
    if (
      !document.fullscreenElement
    ) {
      viewerRef.current?.requestFullscreen();
    } else {
      document.exitFullscreen();
    }
  }

  useEffect(() => {
    function handleFullscreenChange() {
      setIsFullscreen(
        document.fullscreenElement ===
          viewerRef.current
      );
    }

    document.addEventListener(
      "fullscreenchange",
      handleFullscreenChange
    );

    return () => {
      document.removeEventListener(
        "fullscreenchange",
        handleFullscreenChange
      );
    };
  }, []);

  /*
  |--------------------------------------------------------------------------
  | Keyboard shortcuts
  |--------------------------------------------------------------------------
  */

  useEffect(() => {
    function handleKeyboard(
      event
    ) {
      const tag =
        event.target?.tagName;

      /*
       * Search input handles its own keys
       */
      if (
        tag === "INPUT" ||
        tag === "TEXTAREA"
      ) {
        return;
      }

      if (
        event.key === "ArrowLeft"
      ) {
        previousPage();
      }

      if (
        event.key === "ArrowRight"
      ) {
        nextPage();
      }

      if (
        event.key === "+" ||
        event.key === "="
      ) {
        zoomIn();
      }

      if (event.key === "-") {
        zoomOut();
      }

      if (event.key === "0") {
        resetZoom();
      }

      /*
       * Ctrl + F
       */
      if (
        (event.ctrlKey ||
          event.metaKey) &&
        event.key.toLowerCase() ===
          "f"
      ) {
        event.preventDefault();

        setSearchOpen(true);

        setTimeout(() => {
          searchInputRef.current?.focus();
        }, 50);
      }
    }

    window.addEventListener(
      "keydown",
      handleKeyboard
    );

    return () => {
      window.removeEventListener(
        "keydown",
        handleKeyboard
      );
    };
  }, [
    numPages,
  ]);

  /*
  |--------------------------------------------------------------------------
  | Search input keyboard
  |--------------------------------------------------------------------------
  */

  function handleSearchKeyDown(
    event
  ) {
    if (
      event.key === "Enter"
    ) {
      event.preventDefault();

      if (event.shiftKey) {
        goToPreviousMatch();
      } else {
        goToNextMatch();
      }
    }

    if (
      event.key === "Escape"
    ) {
      setSearchOpen(false);
      setSearchText("");
    }
  }

  /*
  |--------------------------------------------------------------------------
  | Download
  |--------------------------------------------------------------------------
  */

  function downloadPdf() {
    if (!pdfFile) return;

    const link =
      document.createElement("a");

    link.href = pdfFile;
    link.download =
      "document.pdf";

    document.body.appendChild(
      link
    );

    link.click();

    link.remove();
  }

  /*
  |--------------------------------------------------------------------------
  | Render
  |--------------------------------------------------------------------------
  */

  return (
    <div
      ref={viewerRef}
      className="
        flex h-screen w-full
        flex-col overflow-hidden
        bg-slate-100
      "
    >

      {/* ====================================================== */}
      {/* TOOLBAR */}
      {/* ====================================================== */}

      <header
        className="
          z-50 flex h-14
          shrink-0 items-center
          justify-between
          border-b border-slate-200
          bg-white px-3 shadow-sm
        "
      >

        {/* LEFT */}

        <div className="
          flex min-w-0
          items-center gap-3
        ">
          <div
            className="
              flex h-9 w-9
              shrink-0 items-center
              justify-center
              rounded-lg bg-red-500
              text-xs font-bold
              text-white
            "
          >
            PDF
          </div>

          <div className="hidden sm:block">
            <p className="
              text-sm font-semibold
              text-slate-800
            ">
              PDF Document
            </p>

            <p className="
              text-xs text-slate-400
            ">
              {numPages
                ? `${numPages} pages`
                : "Loading..."}
            </p>
          </div>
        </div>

        {/* CENTER */}

        <div
          className="
            absolute left-1/2
            flex -translate-x-1/2
            items-center gap-1
          "
        >
          <IconButton
            onClick={
              previousPage
            }
            disabled={
              pageNumber <= 1
            }
            title="Previous page"
          >
            <ChevronLeft
              size={18}
            />
          </IconButton>

          <div
            className="
              flex h-9
              items-center
              rounded-lg border
              border-slate-200
              bg-slate-50 px-2
            "
          >
            <input
              type="number"
              value={pageNumber}
              min={1}
              max={
                numPages || 1
              }
              onChange={
                handlePageChange
              }
              className="
                w-9 bg-transparent
                text-center
                text-sm outline-none
              "
            />

            <span className="
              px-1 text-sm
              text-slate-400
            ">
              /
            </span>

            <span className="
              min-w-5 text-sm
              text-slate-600
            ">
              {numPages || "-"}
            </span>
          </div>

          <IconButton
            onClick={
              nextPage
            }
            disabled={
              !numPages ||
              pageNumber >= numPages
            }
            title="Next page"
          >
            <ChevronRight
              size={18}
            />
          </IconButton>
        </div>

        {/* RIGHT */}

        <div className="
          flex items-center gap-1
        ">

          {/* SEARCH */}

          <IconButton
            onClick={() => {
              setSearchOpen(
                (value) => !value
              );

              setTimeout(() => {
                searchInputRef
                  .current
                  ?.focus();
              }, 50);
            }}
            title="Search"
          >
            <Search size={18} />
          </IconButton>

          {/* ZOOM */}

          <div
            className="
              hidden items-center
              rounded-lg border
              border-slate-200
              bg-slate-50 md:flex
            "
          >
            <IconButton
              onClick={zoomOut}
              disabled={
                scale <= MIN_SCALE
              }
              border={false}
            >
              <Minus size={16} />
            </IconButton>

            <button
              onClick={
                resetZoom
              }
              className="
                min-w-14 px-2
                text-xs font-medium
                text-slate-600
              "
            >
              {Math.round(
                scale * 100
              )}
              %
            </button>

            <IconButton
              onClick={zoomIn}
              disabled={
                scale >= MAX_SCALE
              }
              border={false}
            >
              <Plus size={16} />
            </IconButton>
          </div>

          {/* DOWNLOAD */}

          <IconButton
            onClick={
              downloadPdf
            }
            disabled={!pdfFile}
            title="Download"
          >
            <Download
              size={18}
            />
          </IconButton>

          {/* FULLSCREEN */}

          <IconButton
            onClick={
              toggleFullscreen
            }
            title={
              isFullscreen
                ? "Exit fullscreen"
                : "Fullscreen"
            }
          >
            {isFullscreen ? (
              <Minimize
                size={18}
              />
            ) : (
              <Maximize
                size={18}
              />
            )}
          </IconButton>
        </div>
      </header>

      {/* ====================================================== */}
      {/* SEARCH BAR */}
      {/* ====================================================== */}

      {searchOpen && (
        <div
          className="
            z-40 flex h-14
            items-center
            justify-center
            border-b
            border-slate-200
            bg-white px-4
            shadow-sm
          "
        >
          <div
            className="
              flex w-full
              max-w-xl
              items-center
              gap-2
              rounded-lg
              border
              border-slate-300
              bg-slate-50
              px-3
            "
          >
            <Search
              size={17}
              className="
                shrink-0
                text-slate-400
              "
            />

            <input
              ref={
                searchInputRef
              }
              autoFocus
              value={searchText}
              onChange={(event) =>
                setSearchText(
                  event.target.value
                )
              }
              onKeyDown={
                handleSearchKeyDown
              }
              placeholder="
                Search in document...
              "
              className="
                h-10 flex-1
                bg-transparent
                text-sm outline-none
              "
            />

            {/* RESULT COUNT */}

            {searchText && (
              <span className="
                whitespace-nowrap
                text-xs
                text-slate-500
              ">
                {searchResults.length
                  ? `${currentMatch} / ${searchResults.length}`
                  : "No results"}
              </span>
            )}

            {/* PREVIOUS */}

            <button
              onClick={
                goToPreviousMatch
              }
              disabled={
                !searchResults.length
              }
              className="
                rounded-md p-1.5
                text-slate-500
                hover:bg-slate-200
                disabled:opacity-30
              "
              title="Previous match"
            >
              <ChevronUp
                size={17}
              />
            </button>

            {/* NEXT */}

            <button
              onClick={
                goToNextMatch
              }
              disabled={
                !searchResults.length
              }
              className="
                rounded-md p-1.5
                text-slate-500
                hover:bg-slate-200
                disabled:opacity-30
              "
              title="Next match"
            >
              <ChevronDown
                size={17}
              />
            </button>

            {/* CLOSE */}

            <button
              onClick={() => {
                setSearchText("");
                setSearchOpen(false);
              }}
              className="
                rounded-md p-1.5
                text-slate-400
                hover:bg-slate-200
              "
            >
              <X size={17} />
            </button>
          </div>
        </div>
      )}

      {/* ====================================================== */}
      {/* PDF */}
      {/* ====================================================== */}

      <main
        className="
          relative flex-1
          overflow-auto
          bg-slate-200
        "
      >

        {/* LOADING */}

        {loading && (
          <Loading />
        )}

        {/* ERROR */}

        {!loading && error && (
          <ErrorView
            error={error}
            onRetry={
              loadPdf
            }
          />
        )}

        {/* DOCUMENT */}

        {!error &&
          pdfFile && (
            <div
              className="
                flex min-h-full
                justify-center
                p-4 sm:p-8
              "
            >
              <Document
                file={pdfFile}
                onLoadSuccess={
                  handleDocumentLoadSuccess
                }
                loading={null}
              >
                <div
                  className="
                    overflow-hidden
                    rounded-sm
                    bg-white
                    shadow-2xl
                  "
                >
                  <Page
                    pageNumber={
                      pageNumber
                    }
                    scale={scale}
                    renderTextLayer
                    renderAnnotationLayer

                    /*
                     * REAL HIGHLIGHT
                     */
                    customTextRenderer={({
                      str,
                    }) =>
                      highlightText(
                        str
                      )
                    }
                  />
                </div>
              </Document>
            </div>
          )}
      </main>

      {/* ====================================================== */}
      {/* MOBILE ZOOM BAR */}
      {/* ====================================================== */}

      <div
        className="
          flex h-12 shrink-0
          items-center
          justify-center gap-3
          border-t
          border-slate-200
          bg-white md:hidden
        "
      >
        <IconButton
          onClick={zoomOut}
          disabled={
            scale <= MIN_SCALE
          }
        >
          <Minus size={17} />
        </IconButton>

        <button
          onClick={
            resetZoom
          }
          className="
            min-w-12 text-xs
            font-medium
          "
        >
          {Math.round(
            scale * 100
          )}
          %
        </button>

        <IconButton
          onClick={zoomIn}
          disabled={
            scale >= MAX_SCALE
          }
        >
          <Plus size={17} />
        </IconButton>
      </div>
    </div>
  );
}

/*
|--------------------------------------------------------------------------
| Icon Button
|--------------------------------------------------------------------------
*/

function IconButton({
  children,
  onClick,
  disabled = false,
  title,
  border = true,
}) {
  return (
    <button
      type="button"
      onClick={onClick}
      disabled={disabled}
      title={title}
      className={[
        `
        flex h-9 w-9
        items-center justify-center
        rounded-lg
        text-slate-600
        transition
        hover:bg-slate-100
        hover:text-slate-900
        disabled:cursor-not-allowed
        disabled:opacity-30
        `,
        border
          ? "border border-transparent"
          : "",
      ].join(" ")}
    >
      {children}
    </button>
  );
}

/*
|--------------------------------------------------------------------------
| Loading
|--------------------------------------------------------------------------
*/

function Loading() {
  return (
    <div
      className="
        flex h-full
        min-h-[400px]
        items-center
        justify-center
      "
    >
      <div className="text-center">
        <div
          className="
            mx-auto mb-4
            h-10 w-10
            animate-spin
            rounded-full
            border-4
            border-slate-300
            border-t-blue-500
          "
        />

        <p className="
          text-sm text-slate-500
        ">
          Loading PDF...
        </p>
      </div>
    </div>
  );
}

/*
|--------------------------------------------------------------------------
| Error
|--------------------------------------------------------------------------
*/

function ErrorView({
  error,
  onRetry,
}) {
  return (
    <div
      className="
        flex h-full
        min-h-[400px]
        items-center
        justify-center
        p-6
      "
    >
      <div className="
        max-w-sm text-center
      ">
        <div
          className="
            mx-auto mb-4
            flex h-14 w-14
            items-center justify-center
            rounded-full
            bg-red-100
            text-red-500
          "
        >
          <FileText size={26} />
        </div>

        <h3 className="
          text-base font-semibold
          text-slate-800
        ">
          Unable to load PDF
        </h3>

        <p className="
          mt-2 text-sm
          text-slate-500
        ">
          {error}
        </p>

        <button
          onClick={onRetry}
          className="
            mt-5 inline-flex
            items-center gap-2
            rounded-lg
            bg-slate-900
            px-4 py-2
            text-sm font-medium
            text-white
            hover:bg-slate-700
          "
        >
          <RotateCcw size={15} />
          Try again
        </button>
      </div>
    </div>
  );
}
```

 ### Install

```
npm install react-pdf pdfjs-dist lucide-react
```

 ### Use

```
import PdfViewer from "./PdfViewer";

export default function DocumentPage() {
  const token =
    localStorage.getItem("access_token");

  return (
    <PdfViewer
      documentId="123"
      token={token}
      apiBaseUrl="http://localhost:5000/api/documents"
    />
  );
}
```

 Backend request হবে:

```
GET /api/documents/123/pdf

Authorization: Bearer eyJ...
```

 Backend response:

```
Content-Type: application/pdf
```

 ### Search কীভাবে কাজ করছে

 Flowটা হচ্ছে:

```
Backend PDF
     ↓
PDF.js
     ↓
getTextContent()
     ↓
প্রতিটি page-এর text index
     ↓
User searches "react"
     ↓
Matching pages বের হয়
     ↓
Page automatically changes
     ↓
customTextRenderer()
     ↓
"react" → yellow highlight
```

 একটা বিষয় খেয়াল রাখবেন: **এই implementation text-based PDF-এর জন্য**। Scanned/image-only PDF হলে `getTextContent()`-এ text পাওয়া যাবে না; সেক্ষেত্রে OCR লাগবে।

 আর production-এর জন্য বড় PDF হলে আমি `সব page একসাথে text index` না করে **lazy search indexing + page thumbnails/sidebar + virtualized continuous scrolling** ব্যবহার করব—তাহলে 500–1000 page-এর PDF-ও অনেক smoother থাকবে।

