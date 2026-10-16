# Collimator + spatial filter calculator

Interactive calculator for a Keplerian beam expander with a pinhole spatial filter (laser → L1 → pinhole → L2).
Thai / English toggle, live optical layout, beam-size-vs-distance chart, equations with substituted values, and SVG export.

**Open:** https://saetiew.github.io/collimator-calculator/

## Inputs
Wavelength, input beam diameter (1/e²), M², laser power, f1, pinhole diameter, f2, lens aperture, working distance.

## Outputs
Collimated beam diameter, collimated range (2 z_R), divergence, focal spot size, pinhole transmission and recommended size,
lens clipping, output power, L2/pinhole position tolerance, and the f2 needed for a given working distance.

## Assumptions
Gaussian beam with M² scaling; output waist at L2; recommended pinhole d ≈ λ f1 / (D_in/2) ≈ 1.57 × focal spot.

Single self-contained `index.html` — no build step.
