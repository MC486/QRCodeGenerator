## QR Code Generator with TinyURL Integration
### Overview
This project is a Python-based tool that generates QR codes from URLs, integrates with the TinyURL API to shorten URLs, and optionally adds custom images (like logos) to the QR codes. The generated QR codes are saved as images and logged into an Excel file along with the original and shortened URLs.

#### Features
1. URL Shortening: Automatically shortens URLs using the TinyURL API before encoding them into QR codes.
2. High-Error Correction QR Codes: Generates QR codes with high error correction, ensuring they remain scannable even with modifications or added logos.
3. Customizable Logos: Allows adding a custom logo to the center of the QR code.
4. Image Cropping and Tiling: Crops unnecessary whitespace from the QR codes and tiles them for integration with custom shapes.
5. Excel Integration: Saves details of the generated QR codes, including the user input, original URL, shortened URL, and the QR code image, into an Excel file.
6. Mickey Mouse Template: Optionally overlays the generated QR code with a Mickey Mouse-shaped template for a unique design.

#### Prerequisites
- Python 3.x
- requests library: For interacting with the TinyURL API.
- segno library: For generating QR codes.
- Pillow (PIL) library: For image manipulation.
- openpyxl library: For Excel file manipulation.

#### Installation
##### Clone the repository:
git clone https://github.com/your-username/QRCodeGenerator.git
cd QRCodeGenerator

##### Install the required Python packages:
pip install requests segno Pillow openpyxl
Place your TinyURL API token in a file named tinyurl_auth_token.txt.

###### Add your custom images (sweeping-mickey.png and mickey_template.png) to the project directory.

###### Usage
Run the Script:
python QRCodeGenerator.py
Input the URL: When prompted, enter the URL or data you want to encode in the QR code.

###### Specify the File Name: Enter the desired file name for the final QR code image.

###### View the Results: The generated QR code image will be saved in the project directory. Details including the original URL, shortened URL, and the QR code image will be logged into tinyurl_links.xlsx.

###### Code Breakdown
- read_auth_token(file_path): Reads the TinyURL authentication token from a file.
- shorten_url_with_tinyurl(url): Shortens a given URL using the TinyURL API.
- generate_qr_code_with_high_error_correction(data, scale=10, include_logo=False, logo_path=None): Generates a QR code with optional logo insertion.
- crop_whitespace(image_path): Removes extra whitespace from the QR code image.
- tile_qr_code(cropped_img, tile_count=3): Tiles the cropped QR code for integration with custom shapes.
- overlay_center_qr(tiled_img, center_qr): Overlays a logo-inserted QR code onto the tiled QR image.
- save_to_excel(file_name, xlsx_user_input, xlsx_original_url, xlsx_short_url, xlsx_qr_img): Logs the QR code details into an Excel file.

###### Future Enhancements
- GUI Integration: Implement a graphical user interface for ease of use.
- Dynamic QR Codes: Enable the generation of dynamic QR codes that can be updated without changing the QR code image.
- Bulk URL Processing: Add functionality for bulk processing of URLs from an Excel file.
