# Image-in-a-text-conditioned-scene

Problem Statement

The goal of this project is to place an object’s image into a generated scene using a text prompt. Specifically, the user can generate a background scene using a pre-trained Stable Diffusion model and then overlay a product image (with the background removed) onto that generated scene at a chosen position. This process allows for generating customized, realistic product mockups in various backgrounds based on user-defined prompts.

Project Overview

The project involves:

1. Generating a scene based on a user-provided text prompt using a Stable Diffusion model.
2. Loading a product image and removing its background (specifically the white background).
3. Overlaying the product onto the generated background at a specified position and resizing it for realism.
4. Visualizing and saving the images at each step of the process to ensure clarity and success.

Requirements

Dependencies

To run the project, the following Python packages need to be installed:
pip install torch diffusers transformers accelerate opencv-python Pillow matplotlib numpy

Key Libraries:

torch: Used for handling the Stable Diffusion model.
diffusers: Provides the interface for the Stable Diffusion pipeline.
opencv-python: To handle image processing and manipulation.
Pillow: For handling image files and operations (like removing the background).
matplotlib: For displaying the images at each key step.
numpy: For array operations when modifying image data.

Setup

Clone the repository:
git clone https://github.com/your_username/text-conditioned-object-placement.git
cd text-conditioned-object-placement

Install the required packages:
pip install -r requirements.txt

Download the Stable Diffusion model: The script uses the Stable Diffusion model from HuggingFace, specifically CompVis/stable-diffusion-v1-4. You don't need to manually download it, as it will be fetched automatically.

Prepare your product image: Place your product image (with a white background) in the project folder. Update the image path in the script if necessary.

Modify the prompt for scene generation: In the script, customize the scene_prompt variable to describe the kind of background you want to generate, e.g., "A dense forest with sunlight filtering through the trees.".

Usage

Run the script:
python main.py

The script performs the following steps:

1. Generates a background image based on your text prompt.
2. Loads and removes the white background of the product image.
3. Overlays the product on the generated scene.
4. Displays and saves images after each key step (background generation, background removal, and final combination).
5. Save the output: The final combined image is saved as final_combined_image_realistic.png.

Images Generated at Each Step

1. Important Parts (important_parts.png):
This image shows the steps of the background removal and scene generation processes. It helps visualize the intermediate outputs that are critical for understanding the final result.

Description: It captures different stages of object extraction and background generation. This might include the raw product image, the background, and possibly a mask after the background removal.

2. Final Combined Image (final_combined_image.png):
The initial combination of the product image and the generated background.

Description: This is the merged image where the product (after background removal) is placed onto the generated background, though this step might still need adjustments in terms of realism and sizing.

3. Final Combined Image (Realistic) (final_combined_image_realistic.png):
This is the final, fine-tuned output after the product image has been resized and placed more realistically within the scene.

Description: The final composite image, with a resized product image and adjusted positioning for better realism, such as matching shadows and perspectives.

Customization

Prompt: Modify the scene_prompt to create different backgrounds.
Positioning and Resizing: Adjust the placement coordinates (placement_x, placement_y) and the resize_factor to control where and how large the product appears on the background.

Successful Experiment Images:

![final_combined_image_realistic1](https://github.com/user-attachments/assets/00007276-ce3a-4f09-829f-ffad767b3777)

![final_combined_image_realistic2](https://github.com/user-attachments/assets/ac66add8-a19c-4ac1-9e55-55887451ca88)

![final_combined_image_realistic4](https://github.com/user-attachments/assets/2265337e-6835-40af-8dd7-dce4957633cd)

Failed Experiment Images:

![final_combined_image_realistic3](https://github.com/user-attachments/assets/39964627-f5e9-4d2e-8436-e42541a8dcb3)

![final_combined_image_realistic5](https://github.com/user-attachments/assets/4ca5b9e3-82b6-46ab-9671-9eccc0680d4b)

Approach Breakdown:

1. Environment Setup and Installing Necessary Libraries:
To execute the project, we first installed the following libraries to handle image generation, processing, and model inference:

torch and torchvision: For deep learning framework and model handling.
transformers and diffusers: To work with Hugging Face's models for stable diffusion and text-to-image generation.
opencv-python: For image processing and contour detection.
Pillow: For image manipulation and combining images.
accelerate: For hardware acceleration

Installing these libraries provided the required environment for generating images from text and processing product images.

2. Generating a Scene Based on Text Prompt:
We used the StableDiffusionPipeline from the diffusers library to generate an image based on a specific text prompt. This step allowed us to create a background scene conditioned on the user's input, such as “a kitchen shelf with various cooking utensils.”

Code:
scene_prompt = "A realistic kitchen shelf with various cooking utensils and appliances."
background_image = generate_image(scene_prompt)

The result was an image of a kitchen shelf with items that would normally be present in such a scene.

3. Object Extraction from Product Image:
We uploaded an image of the object (such as a product) and removed its white background. Using OpenCV's contour detection, we extracted the important parts of the image to isolate the object. This allowed us to overlay the object cleanly without background noise.

Code:
product_no_bg = remove_white_background(product_image)

The output here was the object with a transparent background, making it ready for placement into the scene.

4. Overlaying Object on Generated Scene:
We overlaid the object onto the generated background, adjusting the position and resizing the object to fit the scene realistically. We used PIL's paste function to combine both images, creating a natural-looking final image.

Code:
final_image = overlay_images(background_image, product_no_bg, position=(placement_x, placement_y), resize_factor=resize_factor)

The result was a combined image with the object seamlessly placed into the generated scene, such as a kitchen shelf.

5. Using a Different Product Image
If you want to use a different product image for object placement, you need to change the image path in the following sections of the code:
# Set the path to the new product image
product_image = Image.open('path_to_your_new_product_image.png')

# Ensure the new image is passed into the object extraction function
product_no_bg = remove_white_background(product_image)

Make sure the path to the new image is correct and replace it in the code where required. Similarly, you can modify the text prompt for generating a different background scene.

6. Saving and Viewing the Images at Each Step:
At each stage of the process, we saved and displayed the images to monitor progress and ensure the solution was functioning correctly.

Important Parts: Extracted the object with transparent background, ready for integration.
Final Combined Image: The product was placed onto the generated scene.
Final Combined Image Realistic: Further refinement for realistic scaling and positioning of the object.

7. Displaying the image:
plt.imshow(final_image)
plt.show()

Contribution

Contributions are welcome! If you'd like to improve the project, please fork the repository and submit a pull request.
