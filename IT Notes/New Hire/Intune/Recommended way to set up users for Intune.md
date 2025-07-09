

Make their account
Export diagnostics with ctrl + shift +d
Import into Autopilot
Go into Entra > manage MFA > Add TAP > Log into the machine using their username and password > Yes set PIN if your org requires it.
Do everything you need to do on the new hires laptop
Remove it from Entra MFA
Launch CMD as admin
takeown /f "C:\Windows\ServiceProfiles\LocalService\AppData\Local\Microsoft\Ngc" /r /d y
icacls "C:\Windows\ServiceProfiles\LocalService\AppData\Local\Microsoft\Ngc" /grant "%username%:F" /t
Change username above within %'s

cd C:\Windows\ServiceProfiles\LocalService\AppData\Local\Microsoft\Ngc
del /F /S /Q .

Run above as one command


# How to Reset Your PIN in Windows 11 CMD?

[

Tutorials

](https://www.reddit.com/r/Winsides/?f=flair_name%3A%22Tutorials%22)

Resetting your PIN in Windows 11 can be necessary if you've forgotten it or want a fresh start. This guide will help you reset your PIN using **Command Prompt (CMD)** in a straightforward, easy-to-follow process. This method is beneficial when other GUI-based options aren’t available or you prefer using command lines. Let's dive in to learn how to reset your PIN securely through CMD.

# Introduction: Why Resetting PIN Through CMD?

In Windows 11, **Personal Identification Number (PIN)** is commonly used for quick sign-in to enhance security and ease of access. However, there may be situations where you forget the PIN or want to update it for security reasons. The **Command Prompt** method provides an effective way to reset the PIN without navigating multiple windows. This article offers step-by-step instructions for resetting your PIN via CMD, ensuring you're back in control of your Windows account swiftly.

# Steps to Reset PIN in Windows 11 Using CMD

Before proceeding, make sure you have **administrator access** to execute these commands successfully. Here’s how you can reset your PIN with CMD in Windows 11:

# Step 1: Open Command Prompt as Administrator

1. **Press** `Windows + S` to open the **Search** bar.
    
2. Type **cmd** in the search box.
    
3. Right-click on **Command Prompt** and select **Run as administrator**.
    

This will launch the Command Prompt with elevated permissions, necessary for making system changes.

# Step 2: Delete the NGC Folder

The NGC folder in Windows stores your PIN information. By **deleting this folder**, you will remove the current PIN configuration, enabling you to set a new PIN.

1. In the Command Prompt window, type the following command: `cd c:\Windows\ServiceProfiles\LocalService\AppData\Local\Microsoft\Ngc`
    
2. Press **Enter**. This command navigates to the folder containing PIN data.
    
3. Now, enter the following command to delete the folder contents: `del /F /S /Q *.*`
    
    - `/F` forces deletion of read-only files.
        
    - `/S` deletes files from all subdirectories.
        
    - `/Q` operates in quiet mode, skipping confirmation prompts.
        
4. Press **Enter** after typing the command.
    

**Important:** Deleting this folder will reset the PIN for all accounts on this device. Ensure other users are informed if multiple accounts are active.

# Step 3: Set a New PIN

After deleting the NGC folder, follow these steps to set a new PIN:

1. **Restart your computer** by clicking **Start** > **Power** > **Restart**.
    
2. When the system restarts, go to **Settings**:
    
    - Press `Windows + I` to open the **Settings** window.
        
    - Navigate to **Accounts** > **Sign-in options** > **PIN (Windows Hello)**.
        
3. Click on **Add PIN** and follow the instructions to create a new PIN for your account.
    

**Note:** If you are prompted to verify your identity, ensure you have access to your Microsoft account email or phone number for verification.

# Tips for Securing Your New PIN

Resetting your PIN offers an excellent opportunity to create a more secure code. Here are some tips:

- **Use a complex but memorable PIN**: Avoid using simple or sequential numbers like 1234 or 0000.
    
- **Regularly update your PIN** to keep your account secure.
    
- **Enable Two-Factor Authentication (2FA)** if available for added security.
    

# Conclusion: A Simple Yet Effective Method for PIN Reset:

Resetting your PIN in Windows 11 via **Command Prompt** is a reliable way to regain access to your account or simply start afresh. By following these straightforward steps, you can delete your old PIN configuration and create a new, more secure one. This method is especially useful for users comfortable with command-line tools or those experiencing issues with traditional settings based options. Find more interesting tutorials on [https://winsides.com/](https://winsides.com/)

With your new PIN, you’ll have **increased security and peace of mind** on your Windows 11 device. Keep this method in mind for future PIN resets, as it offers a quick and effective solution through the Command Prompt.