# EBS block storage is encrypted and not able to be transported

What happends in this error is that the EBS volume you're trying to transport to the S3 Bucket is encrypted. On the EBS volume options is not possible to change that after its creation, so you will need to do the following process in order to decript that volume:

1. Stop the instance that you need to export;

2. Detach the encrypted EBS Volume;

3. Create a rescue EC2 instance (allow SSH conection), in the same region that the EBS volume is located;

4. Create a new EBS volume with the same configurations of the encrypted one, but on this one do not allow the encryption;

5. Atatch both volumes (the encrypted and not encrypted) in the Rescue Instance;

6. Transfer all the data from the encrypted one to the not encrypted volume;


 *Data transfer from volumes on linux*

    . Log as the root user:

        $ sudo su

    . List all the volumes that are present on that instance

        $ lsblk

    . Transfer all the data from the encypted to the not encrypted volume

        $ dd if=/dev/xvdf of=/dev/xvdg bs=4096 status=progress

        Note: pay attention to the names of the volumes before transfering it.

7. Atatch the Unencrypted volume to the original instance and name it as xvda, so the instance recognize it as the root volume;

# S3 Bucket not listed

Normaly that happens when you create the bucket in a diferent region than the EC2 tha you are trying to transfer. Anyways check the configuration file created on the main export process.

# BLSC-style GRUB found, but unable to detect default kernel

Find the GRUB file, on the following paht ../etc/default/grub and make sure that the GRUB_ENABLE_BLSC parameter is set to false. After changing it to false, set the following command to rebuild the config grub file: 

    $ grub2-mkconfig -o /boot/grub2/grub.cfg

# Parameter error during main process

Check the configuration file, probraly some sintax error, correct the code and try it again.