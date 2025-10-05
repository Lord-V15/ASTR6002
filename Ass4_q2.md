# Question 2: Complete Solution

## Part (i): Surface Area of 1 Parsec Sphere

The surface area of a sphere is A = 4πr²

For r = 1 pc:
- 1 pc = 3.086 × 10¹⁸ cm
- A = 4π(3.086 × 10¹⁸)² = 1.197 × 10³⁸ cm²

**log(A/cm²) = 38.08**

---

## Part (ii): Deriving log Lν Equation

Starting from the AB magnitude definition:
- ABmag = -2.5 log₁₀(fν) - 48.60

Rearranging for fν:
- log₁₀(fν) = -(ABmag + 48.60)/2.5

**Correcting for dust extinction:**
- NUVmag_corr = NUVmag - ANUV = NUVmag - 7.8 × E(B-V)
- log₁₀(fν) = -(NUVmag_corr + 48.60)/2.5

The luminosity is related to flux by:
- Lν = fν × 4πd²
- log Lν = log fν + log(4π) + 2log(d)

**For Coma Cluster (v ≈ 7000 km/s):**

Distance calculation using H₀ = 70 km/s/Mpc:
- d = v/H₀ = 7000/70 = 100 Mpc = 3.086 × 10²⁶ cm
- log(d) = 26.489
- 2log(d) = 52.978
- log(4π) = 1.099

**Full equation:**
```
log Lν = -(NUVmag_corr + 48.60)/2.5 + 1.099 + 52.978
log Lν = -0.4×NUVmag_corr - 19.44 + 1.099 + 52.978
```

**Simplified: log Lν = 34.64 - 0.4×NUVmag_corr** (in erg/s/Hz)

---

## Part (iii): SFR Equation

Given: SFRₙᵤᵥ = 3.5 × 10⁻⁴⁴ × ν × Lν

For NUV band at λ = 235 nm:
- ν = c/λ = (3 × 10¹⁰ cm/s)/(235 × 10⁻⁷ cm) = 1.277 × 10¹⁵ Hz

Therefore:
- SFR = 3.5 × 10⁻⁴⁴ × 1.277 × 10¹⁵ × Lν
- SFR = 4.47 × 10⁻²⁹ × Lν

**Taking logarithms:**
```
log(SFR/M☉/yr) = log(4.47×10⁻²⁹) + log Lν
log(SFR/M☉/yr) = -28.35 + log Lν
```

**Using the equation from part (ii):**
```
log(SFR/M☉/yr) = -28.35 + (34.64 - 0.4×NUVmag_corr)
log(SFR/M☉/yr) = 6.29 - 0.4×NUVmag_corr
```

**This gives SFR values typically in the range 0.01 - 10 M☉/yr for galaxies at z ~ 0.02**

---

## Part (iv): Sample Selection and Calculations

### Sample Selection Criteria:

**Coma Cluster sample:**
- Velocity: 6900 < v < 7100 km/s (narrow range around Coma)
- Position: 194° < RA < 196°, 27° < Dec < 29° (Coma location)
- Your coma_sub file has 62 galaxies ✓

**Field sample (100 Mpc shell):**
- Velocity: 6900 < v < 7100 km/s (same distance)
- Position: Distributed across sky (NOT in Coma region)
- Your shell_sub file has 476 galaxies ✓

**Your samples look correct!**

### Stellar Mass Estimation:

Use K-band luminosity as proxy for stellar mass:
- Absolute K magnitude: Mₖ = k_tc - 5×log₁₀(d/10 pc)
- For d ≈ 100 Mpc: Mₖ = k_tc - 5×log₁₀(10⁸) = k_tc - 40

Stellar mass using mass-to-light ratio:
```
log(M*/M☉) = -0.4×(Mₖ - Mₖ,☉) + log(M/L)ₖ
```

Assuming solar absolute magnitude Mₖ,☉ = 3.28 and (M/L)ₖ ≈ 1:
```
log(M*/M☉) = -0.4×(k_tc - 43.28)
log(M*/M☉) = 17.31 - 0.4×k_tc
```

### Star Formation Rate:

Using the corrected NUV magnitude (column: NUVmag_corr):
```
log(SFR/M☉/yr) = 6.29 - 0.4×NUVmag_corr
```

**Expected SFR range:** For NUVmag_corr between 16-21, you should get log(SFR) between approximately -1.5 to 0.5, corresponding to SFR ~ 0.03 to 3 M☉/yr.

---

## Part (v): CMD and SFMD Features

### Color-Magnitude Diagram (CMD):
**Axes:** (NUV - K) color vs K-band magnitude

**Expected features:**
1. **Blue cloud:** Star-forming galaxies (low NUV-K color, ~2-4)
2. **Red sequence:** Quiescent galaxies (high NUV-K color, ~6-8)
3. **Green valley:** Transition region between blue and red

**Differences between field and cluster:**
- **Coma Cluster:** More galaxies on red sequence (environmental quenching)
- **Field:** More galaxies in blue cloud (ongoing star formation)
- Cluster galaxies generally brighter (more massive galaxies in clusters)

### Star Formation-Mass Diagram (SFMD):
**Axes:** log(SFR) vs log(M*)

**Expected features:**
1. **Main sequence:** Diagonal correlation (log SFR ∝ log M*)
2. **Quenched galaxies:** Low SFR at high masses
3. **Scatter:** ~0.3 dex around main sequence

**Differences:**
- **Coma:** More quenched massive galaxies below main sequence
- **Field:** Tighter main sequence correlation
- Cluster shows stronger mass-dependent quenching

---

## Part (vi): Completeness Mass

The survey is complete for galaxies with L > 10¹⁰ L☉ out to z ~ 0.15.

For v ~ 7000 km/s (z ~ 0.023):
- Distance modulus: μ = 5×log₁₀(d/10pc) = 40
- Apparent K magnitude limit for 10¹⁰ L☉ galaxy:
  - Mₖ ≈ -23 (for 10¹⁰ L☉)
  - k_tc,limit = Mₖ + μ = -23 + 40 = 17

**Completeness mass calculation:**
Using our stellar mass equation:
```
log(M*/M☉) = 17.31 - 0.4×17 = 10.51
```

**The SFMD is complete down to log(M*/M☉) ≈ 10.5** (approximately 3 × 10¹⁰ M☉)

**Supporting evidence:**
- Plot histogram of log(M*) for both samples
- Turnover in distribution indicates incompleteness below ~10¹⁰·⁵ M☉
- Check that galaxies with k_tc > 17 mag become rare

---

## Part (vii): Milky Way and Andromeda Comparison

**Milky Way:**
- SFR = 2 M☉/yr → log(SFR) = 0.30
- M* = 9 × 10¹⁰ M☉ → log(M*) = 10.95

**To compare with our sample, we need to calculate equivalent NUVmag_corr:**
Using log(SFR) = 6.29 - 0.4×NUVmag_corr:
- 0.30 = 6.29 - 0.4×NUVmag_corr
- NUVmag_corr = 14.98

**Position:** On the main sequence, typical star-forming galaxy

**Andromeda (M31):**
- SFR = 0.35 M☉/yr → log(SFR) = -0.46
- M* = 15 × 10¹⁰ M☉ → log(M*) = 11.18

**Equivalent NUVmag_corr:**
- -0.46 = 6.29 - 0.4×NUVmag_corr
- NUVmag_corr = 16.88

**Position:** Below main sequence, partially quenched

**Comparison to sample:**

1. **Mass range:** Both are on the **massive end** of the sample (near or above the completeness limit of log(M*) ~ 10.5)

2. **Milky Way characteristics:**
   - Sits **on the main sequence** with typical SFR for its mass
   - Most field galaxies at log(M*) ~ 11 have SFR ~ 1-5 M☉/yr
   - MW with SFR = 2 M☉/yr is perfectly normal for a field galaxy

3. **Andromeda characteristics:**
   - **Below the main sequence**, showing significant quenching
   - SFR of 0.35 M☉/yr is low for its high mass
   - This behavior is more typical of **cluster galaxies** than field galaxies
   - At M* = 1.5×10¹¹ M☉, typical field galaxies have SFR ~ 3-10 M☉/yr

4. **Physical interpretation:**
   - Andromeda's anomalously low SFR suggests past interactions
   - Known merger history with M32 and M110 may have disrupted star formation
   - Gas depletion from tidal interactions could explain quenching
   - Despite being a field galaxy, M31 behaves like a post-quenching system

5. **Comparison with samples:**
   - **Coma galaxies:** Many show similar quenching to M31 due to environmental effects
   - **Field galaxies:** Most follow main sequence like MW, making M31 unusual
   - The scatter in SFMD shows that while M31 is below average, some field galaxies also show reduced SFR

**Conclusion:** The Milky Way represents a typical star-forming galaxy for its mass in both field and cluster environments. Andromeda is anomalous—despite being a field galaxy, its low specific star formation rate is more characteristic of cluster galaxies, likely due to its unique merger history and gas depletion from gravitational interactions with satellite galaxies.