To exclude specific devices (but not all laptops) from an Intune app deployment policy using a filter, you can create a filter with rule syntax based on specific device attributes, such as device name, model, manufacturer, or other properties available in Intune. Below is a step-by-step guide to create a filter that targets specific devices for exclusion and apply it to your app policy.

### Step 1: Identify Device Attributes for Filtering

Determine the criteria to identify the devices you want to exclude. Common attributes include:

- **Device Name**: (device.deviceName -contains "DEVICE-NAME")
- **Model**: (device.model -eq "Surface Pro 9")
- **Manufacturer**: (device.manufacturer -eq "Dell")
- **Device ID**: (device.deviceId -eq "12345678-1234-1234-1234-1234567890ab")
- **Serial Number**: (device.serialNumber -eq "123456789")
- **OS Version**: (device.osVersion -eq "10.0.19045")

You can find these attributes in the Intune admin center under **Devices** > **All Devices** by selecting a device and reviewing its properties. If you have multiple devices to exclude, you can combine criteria using logical operators (and, or) or create a filter based on a specific pattern.

### Step 2: Create a Filter in Intune

1. **Sign in to the Microsoft Intune Admin Center**: Go to [https://intune.microsoft.com](https://intune.microsoft.com).
2. **Navigate to Filters**:
    - Go to **Tenant administration** > **Filters**.
    - Click **Create** to start a new filter.
3. **Configure the Filter**:
    - **Name and Description**: Use a descriptive name (e.g., "Exclude Specific Devices") and add an optional description.
    - **Platform**: Select the platform of the devices (e.g., Windows, iOS/iPadOS, Android).
    - **Filter Type**: Choose **Exclude** to exclude devices matching the criteria from the policy.
    - **Rule Syntax**: Enter the rule to target specific devices. Examples:
        - **Single device by name**: (device.deviceName -eq "CORP-LAPTOP-01")
        - **Multiple devices by name pattern**: (device.deviceName -startsWith "CORP-LAPTOP")
        - **Specific model**: (device.model -eq "Surface Pro 9")
        - **Multiple conditions**: (device.model -eq "Surface Pro 9" or device.deviceName -eq "CORP-LAPTOP-01")
        - Use the **Expression Builder** for guidance or manually enter the syntax. For complex rules, use the raw expression editor.
    - **Preview Devices**: Click **Preview** to test the filter against enrolled devices to ensure it targets the correct ones.
4. **Save the Filter**: Click **Next**, review, and then **Create** to save the filter.

### Step 3: Apply the Filter to the App Policy

1. **Navigate to the App**:
    - Go to **Apps** > **All Apps** and select the app with the policy you want to modify.
2. **Edit Assignments**:
    - Under **Manage**, select **Properties**, then click **Edit** next to **Assignments**.
    - Find the assignment group (e.g., “All Devices” or a specific device group) under **Required**, **Available**, or **Uninstall**.
3. **Add the Filter**:
    - For the relevant group, click the **Filter** dropdown and select the filter you created (e.g., “Exclude Specific Devices”).
    - Ensure the filter mode is set to **Exclude**.
4. **Save Changes**: Click **Review + Save**, then **Save** to apply the updated assignment. The policy will now exclude the specified devices.

### Example Scenarios

- **Exclude a single device**:
    - Rule: (device.deviceName -eq "CORP-LAPTOP-01")
    - This excludes only the device named “CORP-LAPTOP-01” from the app policy.
- **Exclude devices by model**:
    - Rule: (device.model -eq "Surface Pro 9")
    - This excludes all Surface Pro 9 devices.
- **Exclude multiple specific devices**:
    - Rule: (device.deviceName -eq "CORP-LAPTOP-01" or device.deviceName -eq "CORP-LAPTOP-02")
    - This excludes two specific devices by name.

### Important Notes

- **Attribute Availability**: Not all attributes are available for every platform. Check Microsoft’s documentation for supported filter properties: [https://learn.microsoft.com/en-us/mem/intune/fundamentals/filters#supported-device-properties](https://learn.microsoft.com/en-us/mem/intune/fundamentals/filters#supported-device-properties).
- **Dynamic Evaluation**: Filters evaluate device properties at policy application time. If a device’s attributes (e.g., name or model) change, the filter will re-evaluate accordingly.
- **Combining Filters and Groups**: If your policy already uses group-based exclusions (e.g., for users), ensure there are no conflicts. Filters apply to device assignments, while group exclusions can apply to users or devices.
- **Limitations**: If you need to exclude many devices with no common attribute, consider creating an Azure AD device group instead and excluding it directly in the assignment (as described in your previous question). Filters are better for attribute-based exclusions.
- **Monitoring**: After applying the filter, check **Apps** > **Monitor** > **Device install status** to confirm the targeted devices are excluded.
