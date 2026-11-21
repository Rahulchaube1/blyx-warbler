<img src="assets/logo.png" width="112" height="112" alt="Warbler logo">

# Warbler

Flag sustained clipping while reporting the energy of an audio frame. This Blyx workflow framework is part of the vision, audio and speech collection.

Identical peak readings can represent a single transient or a sustained overload. Inspect run length alongside frame energy. [librosa, frame energy](https://librosa.org/doc/latest/generated/librosa.feature.rms.html)

## Install and run

Install [Blyx 0.2.1](https://www.blyx-lang.space/download) with a Rust toolchain and host linker for native builds.

```sh
git clone --depth 1 --branch v0.1.0 https://github.com/Rahulchaube1/blyx-warbler.git
cd blyx-warbler
blyxc native-run example.blyx
blyxc native-run tests.blyx
```

[Run the editable browser example](https://www.blyx-lang.space/play?example=package-warbler) · [Package page](https://www.blyx-lang.space/packages/warbler) · [Handbook](https://doc.blyx-lang.space/guide/warbler)

## Import the module

Run this in the directory containing your application's entry file.

```sh
git clone --depth 1 --branch v0.1.0 https://github.com/Rahulchaube1/blyx-warbler.git vendor/warbler
```

```blyx
use vendor::warbler::warbler;

fn main() {
    let samples = [1, -1, 0, 0];
    let ceiling = 1.0;
    let allowed = 1.0;
    let result = warbler_meter(samples, ceiling, allowed);
    if len(result) == 0 { println!("invalid"); return; }
    let mut i = 0;
    while i < len(result) {
        println!(at(result, i));
        i += 1;
    }
}
```

Expected output

```text
1
0.5
2
1
```

## API

`warbler_meter(samples, ceiling, allowed)`

Returns [peak, mean square, longest clipped run, alert]. Alert means the longest run exceeded the allowed number of samples. Invalid arguments and nonfinite results return an empty vector. Integers carried in numeric vectors use the exact range from −(2^53−1) to 2^53−1.

| Argument | Domain |
| --- | --- |
| samples | Vector of values, each a finite number |
| ceiling | A positive finite number |
| allowed | A nonnegative exact integer |

## Run the command-line project

Run the example with your own numbers. Vector arguments accept up to 16 comma-separated entries; use `[]` for an empty vector. The imported API accepts longer vectors. Invalid arguments return a nonzero exit status.

```sh
blyxc native-run project.blyx -- "1,-1,0,0" 1 1
```

## Libraries

- [FrameSignal](https://github.com/Rahulchaube1/blyx-framesignal/tree/v0.1.0) — Measure peak amplitude and mean-square energy of a signal frame.
- [ClipRuns](https://github.com/Rahulchaube1/blyx-clipruns/tree/v0.1.0) — Count overloaded samples and the longest continuous run.

This release includes identical copies of both library modules so a tagged clone can build offline.

## Verification and contributions

The regression suite in [tests.blyx](tests.blyx) checks the example, boundary cases and invalid inputs. Include a short reproducer and your compiler version in [an issue](https://github.com/Rahulchaube1/blyx-warbler/issues). The source is dual-licensed under [MIT](LICENSE-MIT) or [Apache-2.0](LICENSE-APACHE). The package artwork uses [Lucide icons](https://lucide.dev/license); see [artwork notices](assets/NOTICE.txt).

## Connect with Rahul Chaube

[Portfolio](https://www.rahulchaube1.com/) · [GitHub](https://github.com/Rahulchaube1) · [LinkedIn](https://www.linkedin.com/in/rahulchaube1) · [Hugging Face](https://huggingface.co/oncody) · [X](https://x.com/RahulChaube_) · [EverestQ](https://www.everestqai.com/) · [Contact](https://www.rahulchaube1.com/contact)

[Blyx website](https://www.blyx-lang.space/) · [BlyxTorch](https://www.blyx-lang.space/packages/blyxtorch) · [Handbook](https://doc.blyx-lang.space/) · [Community](https://www.blyx-lang.space/community)

Support Rahul’s open-source work through [GitHub Sponsors](https://github.com/sponsors/Rahulchaube1) or [Buy Me a Coffee](https://buymeacoffee.com/rahulchaube).
