# Atombytes

An adapter from atoms to bytes.

A hash can only verify bytes. A physical object is atoms. Atombytes is the step in between: capture the object in a repeatable way, reduce the capture to a stable fingerprint, hash the fingerprint, and anchor the hash on a public ledger such as Nostr.

Same object, captured twice, should give the same hash. A different object should not.

## Pipeline

1. Capture: a photo (v0.2). Later: microscope, spectrometer, whatever fits the object.
2. Crop: pick the part of the object that counts, and ignore what changes (contents, background).
3. Normalize: 32x32 greyscale, so two captures look alike.
4. Fingerprint: pHash (DCT, 64 bit) + dHash (gradient, 64 bit) = 128 bits.
5. Hash and anchor: SHA-256 of the fingerprint, emitted as an unsigned Nostr event (kind 1063 style) with the crop box in its tags.

The hard part is stage 4. The rest is plumbing.

## Run

Open `index.html` in a browser. Everything runs client-side; no photo leaves your device.

## Status

v0.2. The adapter is a plain photo plus a manual crop. Two photos of the same object score a Hamming distance under about 16 when the crop is chosen well. v0.3 will fingerprint close-up features only one object has (glass seams, paper fibres, craquelure).

## License

MIT. Copyright Hasky Labs, Copenhagen.
