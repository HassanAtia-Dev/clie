# MuMain Client

كلاينت MuMain (Season 6) — مفصول عن السيرفر.

- **السيرفر:** https://github.com/HassanAtia-Dev/ser
- **الكود المشترك حالياً:** مجلد `client/` من [OpenMU-MuMain](https://github.com/HassanAtia-Dev/OpenMU-MuMain)

## GitHub Actions

كل push/PR يبني:

1. **MuMain x64 Release** (Windows MinGW)
2. **MuMain x86 Release** (Windows MinGW)

ويرفع artifacts: `MuMain-x64-Release` و `MuMain-x86-Release`.

الـ CI بيسحب `client/` من OpenMU-MuMain (sparse checkout) ويستعيد الملفات الناقصة من upstream [sven-n/MuMain](https://github.com/sven-n/MuMain) (GLEW، packet headers، CharMakeWin، UIControls، …).

## البناء المحلي (Windows)

```bash
git clone --depth 1 --filter=blob:none --sparse https://github.com/HassanAtia-Dev/OpenMU-MuMain.git
cd OpenMU-MuMain
git sparse-checkout set client
cd client
git submodule update --init --recursive

# x64
cmake --preset windows-x64
cmake --build --preset windows-x64-release --parallel

# x86
cmake --preset windows-x86
cmake --build --preset windows-x86-release --parallel
```

المتطلبات: CMake 3.25+، Ninja، MinGW أو VS2022، .NET 10 SDK، Python 3.
