# Layer Cake 1/3

## Challenge Overview
- **Points:** 20
- **Original French description:** Un développeur de GoodCorp souhaite publier une nouvelle image Docker. Suite à ses mésaventures avec les Dockerfile, il décide d'utiliser Nix pour construire son image. En utilisant Nix, il donne un flag en argument à un service. Il vous assure que ce secret n'est pas visible du public. L'image est anssi/fcsc2024-forensics-layer-cake-3.
- **Translated Description :** A GoodCorp developer wants to publish a new Docker image. Following their mishaps with Dockerfiles, they decide to use Nix to build their image. Using Nix, they pass a flag as an argument to a service. They assure you that this secret is not visible to the public. The image is `anssi/fcsc2024-forensics-layer-cake-3`.



## Solution

To access the flag in the Docker image, follow these steps:

1. **Save the Docker Image to a Tarball**:
   ```bash
   docker save -o image.tar anssi/fcsc2024-forensics-layer-cake-3
   ```

2. **Extract the Tarball**:
Extract the contents of the tarball to a directory.

3. **View the File**:
Navigate to the directory containing the extracted files and locate the following path:

    ```bash
    Intro\Layer Cake 33\image\b27944d1020a3fe70a1073f9976fe560782794464e6ad85ff6e8982588dad42f\layer\nix\store\m8ww0n3iqndg8zaiwbsnij6rvmpmjbry-hello\bin\hello
    ```

View the contents of the hello file to find the flag.

- **Flag:** 
FCSC{a1240d90ebeed7c6c422969ee529cc3e1046a3cf337efe51432e49b1a27c6ad2}
