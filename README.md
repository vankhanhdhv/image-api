# Text Overlay Image API

This project provides an HTTP API to overlay text onto images with customizations for font size, line height, font weight, and placement. The API allows you to create images with text content dynamically.

## Features
- Accepts an image URL and text content with styling parameters.
- Allows customization of font size, line height, font weight, and text placement.
- Outputs the generated image as a PNG file.

## API Documentation

### Endpoint
`POST: https://<your-domain>/generate`

### Request Body (JSON)
```json
{
  "image_url": "string",
  "contents": [
    {
      "text": "string",
      "font_size": "float",
      "rect": [x1, y1, x2, y2],
      "line_height": "float",
      "color": "hex",
      "font_weight": "string"
    }
  ]
}
```

### Parameters
| Parameter     | Type     | Description                                                                                     |
|---------------|----------|-------------------------------------------------------------------------------------------------|
| `image_url`   | `string` | URL of the base image to be used.                                                              |
| `contents`    | `array`  | An array of text content objects for overlay.                                                  |
| `text`        | `string` | The text to overlay on the image.                                                              |
| `font_size`   | `float`  | The font size for the text (e.g., `12.5`).                                                     |
| `rect`        | `array`  | A rectangle `[x1, y1, x2, y2]` specifying the text area (top-left and bottom-right coordinates).|
| `line_height` | `float`  | Line height multiplier for text spacing (e.g., `1.5`).                                         |
| `color`       | `hex`    | Hexadecimal color code for the text (e.g., `#FFFFFF`).                                         |
| `font_weight` | `string` | Font weight for the text (e.g., `normal`, `bold`, `500`, `700`).                               |

### Example Request
```json
{
  "image_url": "https://example.com/sample.png",
  "contents": [
    {
      "text": "Hello, World!",
      "font_size": 20.0,
      "rect": [50, 100, 400, 200],
      "line_height": 1.5,
      "color": "#000000",
      "font_weight": "bold"
    },
    {
      "text": "Subtitle",
      "font_size": 16.0,
      "rect": [50, 220, 400, 260],
      "line_height": 1.2,
      "color": "#FF5733",
      "font_weight": "500"
    }
  ]
}
```

### Example Response
- **Content-Type:** `image/png`
- **Headers:**
  - `Content-Disposition: attachment; filename="result.png"`
- The body contains the PNG image data.

### Error Handling
| HTTP Status Code | Description                          |
|------------------|--------------------------------------|
| `400`            | Invalid request body or parameters. |
| `500`            | Internal server error.              |

---

## Installation

### Prerequisites
- **Go 1.17+**
- Install required Go modules:
  ```bash
  go get github.com/disintegration/imaging
  go get github.com/golang/freetype
  go get golang.org/x/image/font
  ```

### Setup
1. Clone the repository.
2. Place the required font files in the `./fonts` directory:
   - `Quicksand-Regular.ttf`
   - `Quicksand-Bold.ttf`
   - `Quicksand-Medium.ttf`
3. Run the application:
   ```bash
   go run main.go
   ```
4. The server starts on `http://localhost:8080`.

---

## Additional Information

### Fonts
- The application requires `.ttf` font files. Place the files in the `./fonts` directory.
- Font weights are dynamically selected based on the `font_weight` parameter in the request.

### Customization
- Adjust font size, text placement (`rect`), line height, and font weight to customize the appearance of the text overlay.

### Example Images
Use a sample image and payload to generate overlays with text for testing.

---

## Troubleshooting

### Common Errors
- **Font Not Found:** Ensure all required font files (`Quicksand-Regular.ttf`, `Quicksand-Bold.ttf`, `Quicksand-Medium.ttf`) are placed in the correct directory.
- **Invalid Image URL:** Verify the URL provided for `image_url` is accessible and points to a valid image.