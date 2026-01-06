---
layout: single
title: "CleanPix: Strip Image Metadata Locally, Protect Your Privacy"
date: 2026-01-06
categories: [Android, Open Source]
tags: [markdown, kotlin, jetpack-compose, mobile, android-app]
---

## Why Your Photos Know Too Much About You

Every photo you take with your smartphone contains far more than just the image itself. Hidden in the file is a treasure trove of metadata—GPS coordinates showing exactly where you took the photo, the date and time, your camera model, and even technical details like aperture and ISO settings. This EXIF (Exchangeable Image File Format) data can be incredibly revealing.

Posting a photo of an item you're selling online? You might be broadcasting your home address. Sharing a picture on a forum? You could be revealing when and where you were at a specific moment. While this metadata can be useful for organizing your personal photo library, it becomes a privacy liability the moment you share images with others.

The common solution? Upload your photo to a web service that strips the metadata for you. But this approach has an obvious flaw: you're trusting a third party with your images and hoping they handle your data responsibly.

## The Solution: Local, Private, Transparent

**CleanPix** is a small Android app built around a simple principle: *your photos should never leave your device unless you want them to*.

Instead of uploading images to a cloud service, CleanPix processes everything locally on your phone. Select an image, strip its metadata, and save or share the cleaned version—all without an internet connection. In fact, the app doesn't just avoid requiring internet access; it's literally *incapable* of connecting to the internet at all.

## Privacy-First by Design

When I built CleanPix, privacy wasn't an afterthought—it was the foundation. Here's what that means in practice:

### No Internet Permission

The most important privacy protection is the one you can verify yourself. Open the app's `AndroidManifest.xml` file and you'll notice something missing: there's no `android.permission.INTERNET` permission. Android's permission system is absolute—if an app doesn't request internet permission, it cannot make network connections. Period.

This isn't a promise or a policy. It's a technical guarantee enforced by the operating system. CleanPix cannot send your photos anywhere, cannot phone home with analytics, and cannot check for updates. It's completely offline, by design.

### Minimal Permissions

The app requests exactly one permission on modern Android devices: `READ_MEDIA_IMAGES`. That's it. No access to your contacts, location, camera, microphone, or anything else. Just the ability to read the photos you explicitly select.

On older Android versions (Android 9 and below), the app requests `WRITE_EXTERNAL_STORAGE` to save cleaned images to your device—but again, nothing more than absolutely necessary.

### Zero Tracking

I searched the codebase for any analytics or tracking SDKs—Firebase, Google Analytics, Crashlytics, Mixpanel, anything. The result? Nothing. There are no third-party tracking libraries, no usage statistics, no crash reports sent to remote servers. The app doesn't know who you are, how you use it, or even that you exist.

This is documented in the app's privacy policy, which explicitly states:
- No personal information is collected
- No usage is tracked
- No activity is logged
- No analytics are used
- No account is required
- No internet connection is made

### Local Processing Only

When you select an image in CleanPix, here's what happens:

1. The image is copied to the app's temporary cache directory
2. All processing happens in memory on your device
3. The cleaned image is saved either to your device's Pictures folder or shared directly
4. Temporary files are cleaned up automatically

Your photos never leave your phone. The entire process happens in the app's private storage, isolated from other apps and the internet.

### Open Source Transparency

CleanPix is open source, which means anyone can inspect the code to verify these privacy claims. You don't have to trust me—you can verify for yourself. The entire codebase is available, and the implementation is straightforward enough that even someone with basic programming knowledge can understand what's happening.

## How It Works

The technical implementation is surprisingly simple, which is part of what makes it trustworthy. Here's the process:

### 1. Select an Image

Using Android's built-in photo picker, you select an image from your device. The picker itself is privacy-focused—it doesn't give the app access to your entire photo library, just the specific image you choose.

### 2. Read and Display Metadata

Before stripping anything, CleanPix shows you what metadata exists in your image. This might include:

- **GPS Coordinates**: Latitude, longitude, and altitude
- **Date and Time**: When the photo was taken
- **Camera Information**: Make, model, and software version
- **Technical Details**: Aperture, ISO speed, focal length
- **Other Data**: Artist, copyright, orientation, and more

This transparency lets you understand exactly what information you're removing.

### 3. Strip the Metadata

Here's where the magic happens, and it's beautifully simple. The core implementation in `MetadataStripper.kt:163-206` works like this:

```kotlin
fun stripMetadata(uri: Uri): Result<Uri> {
    // Read the EXIF orientation tag before stripping
    val orientation = readOrientation(uri)

    // Load the image as a bitmap
    val originalBitmap = BitmapFactory.decodeStream(inputStream)

    // Rotate the bitmap data based on the EXIF orientation
    val rotatedBitmap = rotateBitmap(originalBitmap, orientation)

    // Re-encode as JPEG without writing any EXIF data
    FileOutputStream(cleanedFile).use { outputStream ->
        rotatedBitmap.compress(Bitmap.CompressFormat.JPEG, 100, outputStream)
    }

    return Result.success(Uri.fromFile(cleanedFile))
}
```

The key insight: when you re-encode an image as JPEG without explicitly copying the EXIF data, all metadata is automatically discarded. The app preserves the correct image rotation by reading the EXIF orientation tag first, rotating the actual bitmap data, and then saving the rotated image without any metadata.

### 4. Verify the Results

CleanPix shows you a side-by-side comparison: your original image with all its metadata, and the cleaned version. If the cleaning was successful, you'll see "All metadata removed!" where the metadata list used to be.

### 5. Save or Share

Finally, you can save the cleaned image to your device (stored in `Pictures/CleanPix/`) or share it directly using Android's share sheet. Either way, you're sharing a clean image with zero privacy-revealing metadata.

## Additional Safeguards

Beyond the core functionality, CleanPix includes several protective measures:

- **Size Limits**: Images are capped at 25MB and 8192×8192 pixels to prevent memory issues
- **Format Validation**: Only JPEG and PNG images are accepted
- **Error Handling**: Clear, user-friendly error messages explain what went wrong
- **Quality Preservation**: Images are re-encoded at 100% quality to minimize visual degradation

## Why This Matters

The implications of photo metadata might seem abstract until you consider real-world scenarios:

- **Selling Items Online**: Posting a photo of something you're selling on Craigslist or Facebook Marketplace could reveal your home address through GPS coordinates.

- **Social Media Privacy**: Even if you're careful about what you post, metadata can reveal patterns about where you spend time and when.

- **Camera Fingerprinting**: The unique combination of camera make, model, and settings can be used to link photos together, potentially connecting your anonymous posts to your real identity.

- **Simple Peace of Mind**: Sometimes you just want to share a photo without worrying about what information you're inadvertently including.

Privacy shouldn't require technical expertise or blind trust in third-party services. With CleanPix, you have a simple, transparent tool that solves a real problem without introducing new privacy risks.

## The Bigger Picture

CleanPix represents a philosophy: privacy tools should be small, focused, and verifiable. They should do one thing well, with minimal permissions and maximum transparency. They shouldn't require an account, shouldn't phone home, and shouldn't collect data "for your convenience."

Most importantly, they should give you control. Your photos, processed on your device, with no intermediaries and no trust required. It's a small app, but it demonstrates that privacy-respecting software doesn't have to be complicated or compromised.

## Try It Yourself

CleanPix is available as open source. You can review the code, build it yourself, or use it as a reference for your own privacy-focused projects. The implementation is straightforward, the architecture is modern (Kotlin + Jetpack Compose), and the privacy guarantees are verifiable.

Because when it comes to your privacy, you shouldn't have to take anyone's word for it—not even mine.

---

*Interested in the technical details? Check out the [CleanPix repository](https://github.com/harrisonog/CleanPix) to see the full implementation, including comprehensive unit tests that verify metadata removal works correctly.*
