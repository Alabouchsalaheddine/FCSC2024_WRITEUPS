# Layer Cake 1/3

## Challenge Overview
- **Points:** 20
- **Original French description:** Un développeur de GoodCorp souhaite publier une nouvelle image Docker. Il copie au moment du build un fichier contenant un flag, puis le supprime. Il vous assure que ce secret n'est pas visible du public. L'image est anssi/fcsc2024-forensics-layer-cake-2.
- **Translated Description :** A GoodCorp developer wants to publish a new Docker image. They copy a file containing a flag during the build process and then delete it. They assure you that this secret is not visible to the public. The image is anssi/fcsc2024-forensics-layer-cake-2.



## Solution

docker save -o image.tar anssi/fcsc2024-forensics-layer-cake-2



To access intermediate layers of a Docker image, you can use the `docker save` command to export the image to a tarball, and then you can manually inspect the contents of each layer. Here's a step-by-step guide:

1. **Save the Docker Image to a Tarball**:
   
   Run the following command to save the Docker image to a tarball:

   ```bash
   docker save -o image.tar <image_name_or_id>
   ```

   Replace `<image_name_or_id>` with the name or ID of the Docker image you want to inspect.

2. **Extract the Tarball**:
   
   Extract the tarball into a directory using the following command:

   ```bash
   mkdir image_contents
   tar -xf image.tar -C image_contents
   ```

   This command will extract the contents of the tarball into the `image_contents` directory.

3. **Inspect the Layers**:
   
   Navigate to the `image_contents` directory and list its contents. You'll see files corresponding to each layer of the Docker image.

   ```bash
   cd image_contents
   ls
   ```

   You'll see files named `layer.tar` corresponding to each layer. These are the layers of the Docker image.

4. **Extract Files from Intermediate Layers**:

   You can inspect the contents of each layer by extracting the `layer.tar` files. For example, to extract the contents of the first layer:

   ```bash
   tar -xf <path_to_first_layer_tar_file> -C layer1_contents
   ```

   Replace `<path_to_first_layer_tar_file>` with the actual path to the `layer.tar` file corresponding to the first layer.

   After extraction, you can explore the contents of the `layer1_contents` directory to see the files and directories present in that layer.

Repeat the extraction process for each layer to inspect the contents of the intermediate layers. This way, you can access and examine the files present in each layer of the Docker image, including files that were added or removed during the image build process.

Search for : FCSC{ in all the files :

**Flag:** 
FCSC{b38095916b2b578109cbf35b8be713b04a64b2b2df6d7325934be63b7566be3b}

