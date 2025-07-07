# DeepFilterNet Inference-Only

[![Rust CI](https://github.com/YOUR_USERNAME/DeepFilterNet-Infer/workflows/CI/badge.svg)](https://github.com/YOUR_USERNAME/DeepFilterNet-Infer/actions)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![License: Apache 2.0](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](https://opensource.org/licenses/Apache-2.0)

A streamlined, **inference-only** version of [DeepFilterNet](https://github.com/Rikorose/DeepFilterNet) for real-time speech enhancement and noise suppression.

**This fork focuses purely on inference** - all training, dataset creation, and Python dependencies have been removed for a lightweight, fast deployment.

## Features

- **Real-time audio processing** with minimal latency
- **Pure Rust implementation** - no Python dependencies
- **Lightweight** - only inference code, no training overhead
- **Multiple model support** - DeepFilterNet2, DeepFilterNet3, and low-latency variants
- **Cross-platform** - Linux, macOS, and Windows support
- **Optimized builds** - release profiles for maximum performance

## Quick Start

### Prerequisites

- [Rust](https://rustup.rs/) (1.70 or later)
- Audio system libraries:
  - **Linux**: `libasound2-dev`
  - **macOS**: Built-in CoreAudio
  - **Windows**: Built-in audio APIs

### Build and Run

```bash
# Clone this repository
git clone https://github.com/YOUR_USERNAME/DeepFilterNet-Infer.git
cd DeepFilterNet-Infer

# Install audio dependencies (Linux only)
sudo apt-get install libasound2-dev

# Build the demo (real-time audio processing)
cargo build --release -p df-demo --bin df-demo-c

# Run real-time demo
./target/release/df-demo-c
```

## Project Structure

```
DeepFilterNet-Infer/
├── libDF/          # Core DeepFilterNet library (inference only)
├── demo/           # Real-time audio demo application
├── models/         # Pre-trained model files (.tar.gz)
└── target/         # Build outputs
```

## Usage Examples

### Real-time Audio Processing

The demo application processes audio in real-time from your microphone:

```bash
cargo run --release -p df-demo --bin df-demo-c

RUST_LOG=info cargo run --release -p df-demo --bin df-demo-c
```

### Audio Controls (Runtime)

While the demo is running, you can adjust parameters:

- **Attenuation Limit**: Controls maximum noise reduction
- **Post-filter Beta**: Fine-tunes post-processing
- **Threshold Controls**: Adjusts noise detection sensitivity

### Programmatic Usage

```rust
use df::tract::*;

let df_params = DfParams::default(); // Uses built-in DeepFilterNet3
let r_params = RuntimeParams::default_with_ch(1); // Mono audio
let mut model = DfTract::new(df_params, &r_params)?;

// Process audio frame
let enhanced_audio = model.process(&noisy_audio_frame)?;
```

## Configuration

### Model Selection

The project includes embedded models, but you can use custom ones:

## Citation

If you use this inference implementation, please cite the original DeepFilterNet papers:

```bibtex
@inproceedings{schroeter2022deepfilternet,
  title={{DeepFilterNet}: A Low Complexity Speech Enhancement Framework for Full-Band Audio based on Deep Filtering},
  author = {Schröter, Hendrik and Escalante-B., Alberto N. and Rosenkranz, Tobias and Maier, Andreas},
  booktitle={ICASSP 2022 IEEE International Conference on Acoustics, Speech and Signal Processing (ICASSP)},
  year={2022},
  organization={IEEE}
}
```

For DeepFilterNet3:

```bibtex
@inproceedings{schroeter2023deepfilternet3,
  title = {{DeepFilterNet}: Perceptually Motivated Real-Time Speech Enhancement},
  author = {Schröter, Hendrik and Rosenkranz, Tobias and Escalante-B., Alberto N. and Maier, Andreas},
  booktitle={INTERSPEECH},
  year = {2023},
}
```

## License

This project is dual-licensed under either:

- **MIT License** ([LICENSE-MIT](LICENSE-MIT) or [http://opensource.org/licenses/MIT](http://opensource.org/licenses/MIT))
- **Apache License, Version 2.0** ([LICENSE-APACHE](LICENSE-APACHE) or [http://www.apache.org/licenses/LICENSE-2.0](http://www.apache.org/licenses/LICENSE-2.0))

## Acknowledgments

- Original [DeepFilterNet](https://github.com/Rikorose/DeepFilterNet) by Hendrik Schröter and team
- This fork was created to provide a lightweight, inference-only version for production use
