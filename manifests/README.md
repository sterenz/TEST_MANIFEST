# Manifests

To better understand the structure and functionality of your IIIF manifest with annotations and ranges, let's break down the key components and relationships:

### Manifest Structure

1. **Manifest Header:**

   - **`@context`**: Defines the IIIF Presentation API version.
   - **`id`**: The URL where the manifest is located.
   - **`type`**: Specifies that this is a `Manifest`.
   - **`label`**: A human-readable title for the manifest.
   - **`metadata`**: Additional descriptive metadata.
   - **`summary`**: A brief description of the manifest content.
   - **`rights`**: Licensing information.
   - **`requiredStatement`**: Attribution statement.

2. **Canvas Items:**
   Each `Canvas` represents a page in the book and contains:

   - **`id`**: Unique identifier for the canvas.
   - **`type`**: Specifies the type as `Canvas`.
   - **`label`**: A title for the canvas.
   - **`height`** and **`width`**: Dimensions of the canvas.
   - **`items`**: An array of `AnnotationPage` items for painting images on the canvas.
   - **`annotations`**: An array of `AnnotationPage` items for other types of annotations, like comments.

3. **AnnotationPages and Annotations:**

   - **`AnnotationPage`**: Contains multiple `Annotation` items.
   - **`Annotation`**: Includes the details of the annotation, such as the motivation, body, and target.

4. **Structures (Ranges):**
   - **`Range`**: Defines a hierarchical structure to organize canvases into sections (e.g., chapters).
   - **`items`**: Lists canvases or other ranges that belong to this range.

### Example Analysis

Let's take a detailed look at one canvas and its annotations:

#### Canvas Example: `http://ba16551d-981b-4d5e-a452-be3a8d2744db`

- **Label**: "CHAPTER 1 - PAGE 1"
- **Items (Painting Annotations)**:

  ```json
  {
    "id": "http://ba16551d-981b-4d5e-a452-be3a8d2744db/painting",
    "type": "AnnotationPage",
    "items": [
      {
        "id": "http://ba16551d-981b-4d5e-a452-be3a8d2744db/painting/anno",
        "type": "Annotation",
        "motivation": "painting",
        "body": {
          "id": "https://sterenz.github.io/TEST_MANIFEST/images/IIIF-IMAGE-TEST_01/full/full/0/default.jpg",
          "type": "Image",
          "format": "image/jpeg",
          "height": 842,
          "width": 595,
          "service": [
            {
              "id": "https://sterenz.github.io/TEST_MANIFEST/images/IIIF-IMAGE-TEST_01",
              "profile": "level1",
              "type": "ImageService3"
            }
          ]
        },
        "target": "http://ba16551d-981b-4d5e-a452-be3a8d2744db"
      }
    ]
  }
  ```

- **Annotations (Commenting Annotations)**:
  ```json
  {
    "id": "http://ba16551d-981b-4d5e-a452-be3a8d2744db/commenting",
    "type": "AnnotationPage",
    "items": [
      {
        "id": "http://localhost:8888/annotation/1713179240133",
        "type": "Annotation",
        "motivation": "commenting",
        "body": {
          "type": "TextualBody",
          "value": "CHAPTER 1",
          "language": "en",
          "format": "text/plain"
        },
        "target": {
          "source": "http://ba16551d-981b-4d5e-a452-be3a8d2744db",
          "selector": {
            "type": "FragmentSelector",
            "value": "xywh=26,26,166,39"
          }
        },
        "created": "2024-04-15T13:07:20",
        "modified": "2024-04-29T12:05:59"
      },
      {
        "id": "http://localhost:8888/annotation/1714384788083",
        "type": "Annotation",
        "motivation": "commenting",
        "body": {
          "type": "TextualBody",
          "value": "Page 1",
          "language": "en",
          "format": "text/plain"
        },
        "target": {
          "source": "http://ba16551d-981b-4d5e-a452-be3a8d2744db",
          "selector": {
            "type": "FragmentSelector",
            "value": "xywh=31,68,87,35"
          }
        },
        "created": "2024-04-29T11:59:48",
        "modified": "2024-04-29T12:05:59"
      },
      {
        "id": "http://localhost:8888/annotation/1714400222479",
        "type": "Annotation",
        "motivation": "commenting",
        "body": {
          "type": "TextualBody",
          "value": "circle",
          "language": "en",
          "format": "text/plain"
        },
        "target": {
          "source": "http://ba16551d-981b-4d5e-a452-be3a8d2744db",
          "selector": {
            "type": "FragmentSelector",
            "value": "xywh=19,100,540,585"
          }
        },
        "created": "2024-04-29T16:17:02",
        "modified": "2024-04-29T16:17:02"
      },
      {
        "id": "http://localhost:8888/annotation/1714485398417",
        "type": "Annotation",
        "motivation": "commenting",
        "body": {
          "type": "TextualBody",
          "value": "draw",
          "language": "en",
          "format": "text/plain"
        },
        "target": {
          "source": "http://ba16551d-981b-4d5e-a452-be3a8d2744db",
          "selector": {
            "type": "FragmentSelector",
            "value": "xywh=76,151,113,97"
          }
        },
        "created": "2024-04-30T15:56:38",
        "modified": "2024-04-30T15:56:38"
      },
      {
        "id": "http://localhost:8888/annotation/1714487561352",
        "type": "Annotation",
        "motivation": "commenting",
        "body": {
          "type": "TextualBody",
          "value": "Prova",
          "language": "en",
          "format": "text/plain"
        },
        "target": {
          "source": "http://ba16551d-981b-4d5e-a452-be3a8d2744db",
          "selector": {
            "type": "FragmentSelector",
            "value": "xywh=326,30,216,200"
          }
        },
        "created": "2024-04-30T16:32:41",
        "modified": "2024-04-30T16:32:41"
      }
    ]
  }
  ```

### Understanding the Range

#### Range Example: `http://example.org/iiif/book1/range/book`

- **Label**: "Book"
- **Items**:
  - **Chapter 1**:
    - **Label**: "Chapter 1"
    - **Items**:
      - Canvas IDs: `http://ba16551d-981b-4d5e-a452-be3a8d2744db`, `http://95fd2a03-0f2e-480f-8b5e-a086af481b3c`, `http://27a5440a-0710-41a8-a309-033b15af3f44`
  - **Chapter 2**:
    - **Label**: "Chapter 2"
    - **Items**:
      - Canvas IDs: `http://9eee6795-e847-455c-b713-60834e6314b9`, `http://408be70b-8d61-4f8c-ba0d-30f0c3c6e159`

### Key Points

- **Canvas** represents individual pages.
- **Annotations** can be of different motivations (e.g., `painting`, `commenting`) and can target specific areas on a canvas using selectors.
- **Ranges** organize canvases into logical groupings (e.g., chapters).

By examining these components, you can ensure that each part of your manifest is correctly structured and linked, making it functional in IIIF viewers like Mirador.
