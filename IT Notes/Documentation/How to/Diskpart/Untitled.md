


## Method 3: Use DiskPart to Remove Write Protection on USB

DiskPart allows you to manage drives and efficiently remove write protection from USB devices. Follow these steps:

1. Press `Win + X` and select **Command Prompt (Admin)**.
2. Type `diskpart` and press Enter.
3. Type `list disk` to view connected drives.
4. Select your USB by typing `select disk X` (replace X with your USB’s number).
5. Enter `attributes disk clear readonly`.
6. Exit DiskPart and check the USB.