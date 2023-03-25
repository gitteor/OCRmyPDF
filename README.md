<!-- SPDX-FileCopyrightText: 2014 Julien Pfefferkorn -->
<!-- SPDX-FileCopyrightText: 2015 James R. Barlow -->
<!-- SPDX-License-Identifier: CC-BY-SA-4.0 -->

<img src="docs/images/logo.svg" width="240" alt="OCRmyPDF">

[![Build Status](https://github.com/ocrmypdf/OCRmyPDF/actions/workflows/build.yml/badge.svg)](https://github.com/ocrmypdf/OCRmyPDF/actions/workflows/build.yml) [![PyPI version][pypi]](https://pypi.org/project/ocrmypdf/) ![Homebrew version][homebrew] ![ReadTheDocs][docs] ![Python versions][pyversions]

[pypi]: https://img.shields.io/pypi/v/ocrmypdf.svg "PyPI version"
[homebrew]: https://img.shields.io/homebrew/v/ocrmypdf.svg "Homebrew version"
[docs]: https://readthedocs.org/projects/ocrmypdf/badge/?version=latest "RTD"
[pyversions]: https://img.shields.io/pypi/pyversions/ocrmypdf "Supported Python versions"

OCRmyPDF는 스캔한 PDF 파일에 OCR 텍스트 레이어를 추가하여 검색하거나 복사 붙여넣기 할 수 있습니다.

```bash
ocrmypdf                      # it's a scriptable command line program
   -l eng+fra                 # it supports multiple languages
   --rotate-pages             # it can fix pages that are misrotated
   --deskew                   # it can deskew crooked PDFs!
   --title "My PDF"           # it can change output metadata
   --jobs 4                   # it uses multiple cores by default
   --output-type pdfa         # it produces PDF/A by default
   input_scanned.pdf          # takes PDF input (or images)
   output_searchable.pdf      # produces validated PDF output
```

[최신 변경 사항에 대한 자세한 내용은 릴리스노트에 있습니다.](https://ocrmypdf.readthedocs.io/en/latest/release_notes.html).


## Main features

- 일반 PDF에서 검색 가능한 [PDF/A](https://en.wikipedia.org/?title=PDF/A) 파일 생성
- OCR 텍스트를 이미지 아래에 정확하게 배치하여 쉽게 복사/붙여넣기
- 변환될 원본 이미지의 해상도를 원본 그대로 유지
- 가능한 경우 다른 콘텐츠를 방해하지 않고 "무손실" 작업으로 OCR 정보를 삽입
- PDF 이미지를 최적화하여 종종 입력 파일보다 작은 파일로 생성
- 요청 시 OCR을 수행하기 전에 이미지 기울기 보정 가능
- 입력 및 출력 파일의 유효성 검사
- 사용 가능한 모든 CPU 코어에 작업 분산
- [Tesseract OCR](https://github.com/tesseract-ocr/tesseract) 엔진을 사용하여 [100개 이상의 언어](https://github.com/tesseract-ocr/tessdata) 인식
- 개인 데이터를 비공개로 유지
- 수천 페이지의 파일을 처리할 수 있도록 적절하게 확장
- 수백만 개의 PDF에 대한 테스트 완료

자세한 내용은 [설명서](https://ocrmypdf.readthedocs.io/en/latest/)를 참조하세요.

## Motivation

웹에서 OCR PDF 파일에 대한 무료 도구를 많이 찾아봤지만 그 중 어느 것도 만족스럽지 않았습니다.

- Either they produced PDF files with misplaced text under the image (making copy/paste impossible)
- Or they did not handle accents and multilingual characters
- Or they changed the resolution of the embedded images
- Or they generated ridiculously large PDF files
- Or they crashed when trying to OCR
- Or they did not produce valid PDF files
- On top of that none of them produced PDF/A files (format dedicated for long time storage)

...그래서 나만의 도구를 개발하기로 결정


## Installation

Linux, Windows, macOS 및 FreeBSD가 지원됩니다. x64 및 ARM 모두에 대해 Docker 이미지도 사용할 수 있습니다.

| 운영체제                       | 설치 명령어                   |
| ----------------------------- | ------------------------------|
| Debian, Ubuntu                | ``apt install ocrmypdf``      |
| Windows Subsystem for Linux   | ``apt install ocrmypdf``      |
| Fedora                        | ``dnf install ocrmypdf``      |
| macOS (Homebrew)              | ``brew install ocrmypdf``     |
| macOS (nix)                   | ``nix-env -i  ocrmypdf``      |
| LinuxBrew                     | ``brew install ocrmypdf``     |
| FreeBSD                       | ``pkg install py-ocrmypdf`` |
| Conda                         | ``conda install ocrmypdf``    |
| Ubuntu Snap                   | ``snap install ocrmypdf``     |

설치 단계에 대한 [설명서](https://ocrmypdf.readthedocs.io/en/latest/installation.html)를 참조하세요.


## Languages

OCRmyPDF는 OCR에 Tesseract를 사용하고 해당 언어팩을 사용합니다. Linux 사용자의 경우 종종 언어팩을 제공하는 패키지를 필요로 합니다.

```bash
# 모든 Tesseract 언어팩 목록 표시
apt-cache search tesseract-ocr

# 데비안/우분투 사용자
apt-get install tesseract-ocr-chi-sim  # Example: Install Chinese Simplified language pack

# Arch Linux 사용자
pacman -S tesseract-data-eng tesseract-data-deu # Example: Install the English and German language packs

# brew macOS 사용자
brew install tesseract-lang
```

`-l LANG` 다음 인수를 OCRmyPDF에 전달하여 검색해야 하는 언어에 대한 힌트를 제공 할 수 있습니다. 여러 언어를 요청할 수 있습니다.

OCRmyPDF는 Tesseract 4.1.1+를 지원합니다. 환경변수에서 먼저 찾은 버전을 자동으로 사용합니다. 
Windows에서 Tesseract PATH를 제공하지 않는 경우, 레지스트리에 따라 설치된 가장 높은 버전 번호를 사용합니다.


## Documentation and support

OCRmyPDF가 설치되면 다음과 같이 명령어 및 옵션을 설명하는 기본 제공 도움말에 액세스할 수 있습니다.

```bash
ocrmypdf --help
```

Our [documentation is served on Read the Docs](https://ocrmypdf.readthedocs.io/en/latest/index.html).

Please report issues on our [GitHub issues](https://github.com/ocrmypdf/OCRmyPDF/issues) page, and follow the issue template for quick response.


## Requirements

Python(3.7+) 외에도 OCRmyPDF는 Ghostscript와 Tesseract OCR 설치가 필요합니다. OCRmyPDF는 순수 Python으로 거의 모든 OS에서 실행됩니다. (Linux, macOS, Windows 및 FreeBSD)


## License

OCRmyPDF 소프트웨어는 Mozilla Public License 2.0(MPL-2.0)에 따라 사용이 허가되었습니다. 이 라이선스는 OCRmyPDF를 상업용 및 폐쇄형 소스를 포함하는 다른 코드와 통합하는 것을 허용하지만 OCRmyPDF에 대한 소스 수준 수정 사항을 게시하도록 요청합니다.
