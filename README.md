# Pixel FaceUnlock

## Description

FaceUnlock support implementation for Pixel Devices.

## Usage

1. Clone the repository to vendor/google/faceunlock:

    ```bash
    cd $(ANDROID_TOP)

    git clone https://github.com/SigmaDroid-Project/vendor_google_faceunlock.git -b sigma-14 vendor/google/faceunlock
    ```

2. Include it with your build:

    - Add "include vendor/google/faceunlock/device.mk" to your device tree (e.g. device.mk)

    - If AND ONLY IF your ROM base has the FaceSense Face Unlock implmentation from ParanoidAndroid, apply the following patch to your frameworks/base repo:

    ```From 3438ec86e0d5ebe7f1e632d27d6de90785bc3351 Mon Sep 17 00:00:00 2001
    From: Matt Filetto <matt.filetto@gmail.com>
    Date: Fri, 29 Dec 2023 18:23:25 -0800
    Subject: [PATCH] Fix Pixel FaceUnlock

    ---
    .../android/server/biometrics/sensors/face/FaceService.java   | 4 ++--
    1 file changed, 2 insertions(+), 2 deletions(-)

    diff --git a/services/core/java/com/android/server/biometrics/sensors/face/FaceService.java b/services/core/java/com/android/server/biometrics/sensors/face/FaceService.java
    index ec8ffd96618d..7d93441b1e11 100644
    --- a/services/core/java/com/android/server/biometrics/sensors/face/FaceService.java
    +++ b/services/core/java/com/android/server/biometrics/sensors/face/FaceService.java
    @@ -699,12 +699,12 @@ public void registerAuthenticators(

                mRegistry.registerAll(() -> {
                    final List<ServiceProvider> providers = new ArrayList<>();
    -                /*for (FaceSensorPropertiesInternal hidlSensor : hidlSensors) {
    +                for (FaceSensorPropertiesInternal hidlSensor : hidlSensors) {
                        providers.add(
                                Face10.newInstance(getContext(), mBiometricStateCallback,
                                        hidlSensor, mLockoutResetDispatcher));
                    }
    -                providers.addAll(getAidlProviders());*/
    +                providers.addAll(getAidlProviders());
                    providers.addAll(getSenseProviders());
                    return providers;
                });
    ```

3. Profit!

## Contributing

Contributions are welcome! If you have any ideas, suggestions, or bug reports, please open an issue or submit a pull request.

## Contact

For any questions or inquiries, please contact [matt.filetto@gmail.com](mailto:matt.filetto@gmail.com).
