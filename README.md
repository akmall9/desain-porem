# 🎨 Desain Porem - Custom Ubuntu ISO dengan Cubic

Repository ini berisi asset dan konfigurasi untuk membuat custom Ubuntu ISO dengan desain MacOS-style menggunakan Cubic (Custom Ubuntu ISO Creator). Proyek ini memudahkan kustomisasi Ubuntu dengan mengganti foto, tema, dan tampilan sistem operasi.

## 📋 Daftar Isi

- [Tentang Proyek](#-tentang-proyek)
- [Fitur](#-fitur)
- [Struktur Repository](#-struktur-repository)
- [Prasyarat](#-prasyarat)
- [Cara Penggunaan](#-cara-penggunaan)
- [Kustomisasi](#-kustomisasi)
- [Troubleshooting](#-troubleshooting)
- [Kontributor](#-kontributor)
- [Lisensi](#-lisensi)

## 🎯 Tentang Proyek

Desain Porem adalah proyek kustomisasi Ubuntu yang dibuat oleh Kelompok 5. Proyek ini menggunakan **Cubic (Custom Ubuntu ISO Creator)** untuk membuat distribusi Linux Ubuntu yang sudah dikustomisasi dengan tema MacOS-style, lengkap dengan:

- Theme dan icon pack custom
- Wallpaper pilihan
- Logo boot GRUB custom
- Tampilan visual yang lebih menarik

Dengan repository ini, Anda dapat dengan mudah membuat custom Ubuntu ISO hanya dengan mengganti foto/gambar tertentu sesuai preferensi Anda.

## ✨ Fitur

- 🎨 **Theme MacOS-style**: Elegant Mojave Blur dengan efek transparan
- 🖼️ **Icon Pack**: MacTahoe icon theme untuk tampilan yang konsisten
- 🌄 **Wallpaper Collection**: Koleksi wallpaper berkualitas tinggi
- 🚀 **GRUB Theme**: Boot loader dengan logo custom Mac-style
- 📦 **Easy Customization**: Tinggal ganti file gambar untuk personalisasi
- 🔧 **Cubic Ready**: Siap digunakan dengan Cubic untuk build ISO

## 📁 Struktur Repository

```
desain-porem/
├── Elegant-mojave-blur-left-dark/    # Theme utama dengan efek blur
│   ├── gtk-3.0/                      # Konfigurasi GTK3
│   ├── gtk-4.0/                      # Konfigurasi GTK4
│   └── assets/                       # Asset theme
│
├── MacTahoe-icon-theme               # Icon pack MacOS-style
│   └── icons/                        # Koleksi icon
│
├── MyWallpapers/
│   └── contents/
│       └── images/                   # Koleksi wallpaper
│           ├── background.jpg        # Wallpaper utama
│           ├── lockscreen.jpg        # Wallpaper lock screen
│           └── login.jpg             # Wallpaper login screen
│
├── logo-mac-style/                   # Logo untuk GRUB bootloader
│   ├── logo.png                      # Logo utama (1024x1024)
│   └── logo-small.png                # Logo kecil (512x512)
│
├── slides/                           # Slide instalasi Ubuntu
│   ├── slide1.html
│   ├── slide2.html
│   └── ...
│
├── grub.cfg                          # Konfigurasi GRUB bootloader
└── README.md                         # File dokumentasi ini
```

## 🔧 Prasyarat

### Software yang Diperlukan

1. **Ubuntu 20.04 atau lebih baru** (untuk menjalankan Cubic)
2. **Cubic (Custom Ubuntu ISO Creator)**
   ```bash
   sudo apt-add-repository universe
   sudo apt-add-repository ppa:cubic-wizard/release
   sudo apt update
   sudo apt install --no-install-recommends cubic
   ```
3. **Git** untuk clone repository
   ```bash
   sudo apt install git
   ```

### Hardware Requirements

- **RAM**: Minimal 4GB (Rekomendasi 8GB)
- **Storage**: Minimal 20GB ruang kosong
- **Processor**: Dual-core atau lebih tinggi

### File ISO Ubuntu

Download Ubuntu ISO original dari [ubuntu.com](https://ubuntu.com/download/desktop)

## 🚀 Cara Penggunaan

### 1. Clone Repository

```bash
git clone https://github.com/akmall9/desain-porem.git
cd desain-porem
```

### 2. Buka Cubic

```bash
cubic
```

### 3. Setup Proyek di Cubic

1. **Buat Proyek Baru**
   - Klik "Next"
   - Pilih directory untuk proyek Cubic Anda
   - Select Ubuntu ISO yang sudah di-download

2. **Masuk ke Terminal Chroot**
   - Cubic akan extract ISO dan membuka terminal chroot
   - Di sinilah Anda akan menginstall theme dan melakukan kustomisasi

### 4. Install Theme dan Icon

Dalam terminal chroot Cubic:

```bash
# Copy theme ke system directory
cp -r /path/to/desain-porem/Elegant-mojave-blur-left-dark /usr/share/themes/

# Copy icon pack
cp -r /path/to/desain-porem/MacTahoe-icon-theme /usr/share/icons/

# Set theme sebagai default
gsettings set org.gnome.desktop.interface gtk-theme "Elegant-mojave-blur-left-dark"
gsettings set org.gnome.desktop.interface icon-theme "MacTahoe-icon-theme"
```

### 5. Setup Wallpaper

```bash
# Copy wallpapers
mkdir -p /usr/share/backgrounds/custom
cp /path/to/desain-porem/MyWallpapers/contents/images/* /usr/share/backgrounds/custom/

# Set wallpaper default
gsettings set org.gnome.desktop.background picture-uri "file:///usr/share/backgrounds/custom/background.jpg"
```

### 6. Setup GRUB Theme

```bash
# Copy logo GRUB
cp /path/to/desain-porem/logo-mac-style/logo.png /boot/grub/

# Copy konfigurasi GRUB
cp /path/to/desain-porem/grub.cfg /boot/grub/grub.cfg
```

### 7. Setup Slides Instalasi (Opsional)

```bash
# Copy slides ke directory installer
cp -r /path/to/desain-porem/slides/* /usr/share/ubiquity-slideshow/slides/
```

### 8. Build ISO

1. Keluar dari chroot terminal
2. Lanjutkan wizard Cubic
3. Customize boot configuration jika diperlukan
4. Generate ISO file
5. Tunggu proses selesai

### 9. Test ISO

```bash
# Test dengan QEMU/KVM
qemu-system-x86_64 -cdrom custom-ubuntu.iso -boot d -m 2048
```

Atau burn ke USB menggunakan tools seperti:
- **Etcher** (Cross-platform)
- **Rufus** (Windows)
- **dd command** (Linux)

```bash
# Menggunakan dd (hati-hati dengan device path!)
sudo dd if=custom-ubuntu.iso of=/dev/sdX bs=4M status=progress && sync
```

## 🎨 Kustomisasi

### Mengganti Wallpaper

Untuk mengganti wallpaper, cukup replace file di folder `MyWallpapers/contents/images/`:

```bash
cd MyWallpapers/contents/images/

# Ganti dengan foto Anda sendiri
# Pastikan nama file tetap sama atau update path di script
cp /path/to/your/wallpaper.jpg background.jpg
cp /path/to/your/lockscreen.jpg lockscreen.jpg
cp /path/to/your/login.jpg login.jpg
```

**Rekomendasi Resolusi:**
- Background: 1920x1080 atau lebih tinggi
- Lock Screen: 1920x1080
- Login Screen: 1920x1080

### Mengganti Logo GRUB

```bash
cd logo-mac-style/

# Ganti dengan logo Anda
# Format: PNG dengan background transparan
cp /path/to/your/logo.png logo.png

# Untuk logo kecil
cp /path/to/your/small-logo.png logo-small.png
```

**Spesifikasi Logo:**
- Format: PNG dengan alpha channel (transparan)
- Logo utama: 1024x1024 px
- Logo kecil: 512x512 px

### Mengganti Theme Color

Edit file `Elegant-mojave-blur-left-dark/gtk-3.0/gtk.css`:

```css
/* Ubah warna utama */
@define-color theme_selected_bg_color #007AFF;  /* Warna aksen */
@define-color theme_bg_color #2C2C2C;           /* Background */
@define-color theme_fg_color #FFFFFF;           /* Foreground/text */
```

### Customize Slides Instalasi

Edit file HTML di folder `slides/`:

```bash
cd slides/

# Edit dengan text editor favorit Anda
nano slide1.html
```

Struktur slide:
```html
<!DOCTYPE html>
<html>
<head>
    <title>Slide Title</title>
</head>
<body>
    <h1>Welcome to Custom Ubuntu</h1>
    <p>Your custom message here...</p>
    <img src="images/your-image.jpg" alt="Custom Image">
</body>
</html>
```

### Customize GRUB Configuration

Edit `grub.cfg` untuk mengubah:
- Timeout boot
- Default boot entry
- Menu entries
- Background image

```bash
# Edit grub.cfg
nano grub.cfg
```

Contoh kustomisasi:
```bash
# Set timeout (dalam detik)
set timeout=10

# Set default entry (0 = first entry)
set default=0

# Set background image
background_image /boot/grub/logo.png
```

## 🐛 Troubleshooting

### ISO Tidak Bisa Boot

**Problem**: ISO tidak mau boot di USB atau VM

**Solution**:
1. Pastikan GRUB configuration benar
2. Cek apakah boot mode UEFI/Legacy sesuai
3. Rebuild ISO dengan Cubic
4. Test di VM dulu sebelum burn ke USB

### Theme Tidak Muncul

**Problem**: Theme tidak apply setelah install

**Solution**:
```bash
# Install GNOME Tweaks
sudo apt install gnome-tweaks

# Jalankan dan pilih theme manual
gnome-tweaks
```

### Wallpaper Tidak Berubah

**Problem**: Wallpaper masih default Ubuntu

**Solution**:
```bash
# Set manual dengan gsettings
gsettings set org.gnome.desktop.background picture-uri "file:///usr/share/backgrounds/custom/background.jpg"

# Atau gunakan GUI
# Settings > Background > pilih wallpaper custom
```

### GRUB Logo Tidak Muncul

**Problem**: Logo di boot screen tidak tampil

**Solution**:
1. Cek format file (harus PNG)
2. Cek path di grub.cfg
3. Pastikan file ada di `/boot/grub/`
4. Update GRUB: `sudo update-grub`

### Cubic Crash atau Freeze

**Problem**: Cubic crash saat build ISO

**Solution**:
1. Pastikan ada cukup RAM (minimal 4GB)
2. Tutup aplikasi lain
3. Cek ruang disk tersedia
4. Restart Cubic dan coba lagi

### Permission Denied Errors

**Problem**: Error permission saat copy files

**Solution**:
```bash
# Jalankan dengan sudo
sudo cp -r source destination

# Atau ubah ownership
sudo chown -R $USER:$USER /path/to/directory
```

## 👥 Kontributor

Proyek ini dikembangkan oleh **Kelompok 5**:

- [Akmal](https://github.com/akmall9) - Project Lead & Developer

Ingin berkontribusi? Silakan fork repository ini dan submit pull request!

### Cara Berkontribusi

1. Fork repository
2. Create feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to branch (`git push origin feature/AmazingFeature`)
5. Open Pull Request

## 📄 Lisensi

Project ini menggunakan berbagai komponen dengan lisensi yang berbeda:

- **Theme Elegant-mojave-blur**: Sesuai lisensi original theme
- **MacTahoe Icons**: Sesuai lisensi original icon pack
- **Wallpapers**: Pastikan Anda memiliki hak untuk menggunakan
- **Custom Code**: MIT License (untuk script dan konfigurasi custom)

## 🙏 Acknowledgments

Terima kasih kepada:

- [Cubic Team](https://launchpad.net/cubic) - Tool untuk custom Ubuntu ISO
- [GNOME Project](https://www.gnome.org/) - Desktop environment
- [Ubuntu](https://ubuntu.com/) - Base distribution
- Theme dan icon creators original

## 📞 Support

Jika Anda mengalami masalah atau punya pertanyaan:

- 🐛 [Buat Issue](https://github.com/akmall9/desain-porem/issues)
- 💬 [Discussions](https://github.com/akmall9/desain-porem/discussions)
- 📧 Contact: [GitHub Profile](https://github.com/akmall9)

## 🔗 Resources

- [Cubic Documentation](https://github.com/PJ-Singh-001/Cubic)
- [Ubuntu Documentation](https://help.ubuntu.com/)
- [GNOME Customization Guide](https://wiki.gnome.org/)
- [GRUB Customization](https://www.gnu.org/software/grub/manual/)

---

**⭐ Jika project ini membantu Anda, jangan lupa kasih star di repository ini!**

**📢 Share project ini ke teman-teman yang ingin membuat custom Ubuntu ISO!**

Made with ❤️ by Kelompok 5
