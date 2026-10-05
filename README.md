# Ramp Cat — OSINT Write-up

> **CTF:** Ramp Cat  
> **Category:** Forensics / OSINT  
> **Points:** 100  
> **Flag:** `flag{Koneko}`

---

## Challenge

> Alright. We got a picture of ramp cat. But we can't find him. Find out where he lives for us please?

The objective is to determine where the cat is located and recover the flag.

---

## Initial Investigation

The first thing I did was inspect the image for information that could help identify its location.

Since the challenge asks where the cat **lives**, geographic information was a useful lead to investigate.

Using **ExifTool** to inspect the image metadata revealed GPS information:

```text
GPSLatitude     : 40,43.2257N
GPSLatitudeRef  : N

GPSLongitude    : 73,59.0405W
GPSLongitudeRef : W
```

The coordinates are represented as **degrees + decimal minutes**.

Therefore:

```text
Latitude  = 40° 43.2257′ N
Longitude = 73° 59.0405′ W
```

---

##  Coordinate Conversion

To use the coordinates in a mapping service, I converted them into decimal degrees.

The formula is:

```text
Decimal Degrees = Degrees + (Minutes / 60)
```

### Latitude

```text
40 + (43.2257 / 60)
= 40.7204283
```

### Longitude

The longitude is **West**, so the result is negative:

```text
-(73 + (59.0405 / 60))
= -73.9840083
```

The final coordinates are:

```text
40.7204283, -73.9840083
```

---

## 🗺️ OSINT / Map Investigation

I searched the coordinates using Google Maps:

```text
40.7204283, -73.9840083
```

The coordinates lead to:

```text
26 Clinton St
New York, NY 10002
United States
```

The location is associated with **Koneko**, a cat café.

The connection between the cat-related challenge description and the location gives us the final answer.

---

## 📸 Evidence

### GPS Metadata

The image metadata contains the geographic coordinates used during the investigation.

![GPS Metadata](screenshots/gps-metadata.png)

---

### Image Metadata

Additional metadata from the image was inspected using ExifTool.

![Image Metadata](screenshots/metadata.png)

---

### Google Maps Verification

The converted coordinates were entered into Google Maps and led to the Koneko location.

![Google Maps](screenshots/google-maps.png)

---

## 🚩 Flag

The final flag is:

```text
flag{Koneko}
```

---

## 🛠️ Tools Used

- **ExifTool** — Extracted metadata and GPS information from the image
- **Google Maps** — Used to investigate and verify the coordinates
- **Coordinate conversion** — Converted degrees/minutes into decimal coordinates

---

## Takeaway

This challenge demonstrates a simple but useful OSINT technique:

```text
Image
  ↓
Metadata
  ↓
GPS Coordinates
  ↓
Coordinate Conversion
  ↓
Map Search
  ↓
Location
  ↓
Flag
```

When investigating images in OSINT challenges, don't rely only on the visible content. Always check for potentially useful metadata such as:

- GPS coordinates
- Camera information
- Timestamps
- File names
- Comments
- Embedded metadata

In this case, the GPS metadata provided the direct path to the final location.

---

## 🐈 Final Answer

**`flag{Koneko}`**
