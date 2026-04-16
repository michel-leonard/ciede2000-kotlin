Browse : [Dart](https://github.com/michel-leonard/ciede2000-dart) · [Go](https://github.com/michel-leonard/ciede2000-go) · [JavaScript](https://github.com/michel-leonard/ciede2000-javascript) · [Java](https://github.com/michel-leonard/ciede2000-java) · [Julia](https://github.com/michel-leonard/ciede2000-julia) · **Kotlin** · [Lua](https://github.com/michel-leonard/ciede2000-lua) · [MATLAB](https://github.com/michel-leonard/ciede2000-matlab) · [Microsoft Excel](https://github.com/michel-leonard/ciede2000-excel) · [PHP](https://github.com/michel-leonard/ciede2000-php) · [Perl](https://github.com/michel-leonard/ciede2000-perl)

# CIEDE2000 color difference formula in Kotlin

This page presents the CIEDE2000 color difference, implemented in the Kotlin programming language.

![Logo](https://raw.githubusercontent.com/michel-leonard/ciede2000-color-matching/refs/heads/main/docs/assets/images/logo.jpg)

## About

Here you’ll find the first rigorously correct implementation of CIEDE2000 that doesn’t use any conversion between degrees and radians. Set parameter `canonical` to obtain results in line with your existing pipeline.

`canonical`|The algorithm operates...|
|:--:|-|
`false`|in accordance with the CIEDE2000 values currently used by many industry players|
`true`|in accordance with the CIEDE2000 values provided by [this](https://hajim.rochester.edu/ece/sites/gsharma/ciede2000/) academic MATLAB function|

## Our CIEDE2000 offer

This production-ready file, released in 2026, contain the CIEDE2000 algorithm.

Source File|Type|Bits|Purpose|Advantage|
|:--:|:--:|:--:|:--:|:--:|
[ciede2000.kt](./ciede2000.kt)|`Double`|64|Scientific|Interoperability|

### Software Versions

- OpenJDK 17.0.18
- kotlinc-jvm 2.3.10

### Example Usage

We calculate the CIEDE2000 distance between two colors, first without and then with parametric factors.

```kotlin
fun main() {
	// Example of two L*a*b* colors
	val l1 = 98.8; val a1 = 71.4; val b1 = 6.4;
	val l2 = 93.9; val a2 = 43.4; val b2 = -3.3;

	var delta_e = ciede2000(l1, a1, b1, l2, a2, b2);
	println("CIEDE2000 = " + delta_e); // ΔE2000 = 9.407476583096802

	// Example of parametric factors used in the textile industry
	val kl = 2.0; val kc = 1.0; val kh = 1.0;

	// Perform a CIEDE2000 calculation compliant with that of Gaurav Sharma
	val canonical = true;

	delta_e = ciede2000(l1, a1, b1, l2, a2, b2, kl, kc, kh, canonical);
	println("CIEDE2000 = " + delta_e); // ΔE2000 = 9.067053686706924
}
```

### Test Results

LEONARD’s tests are based on well-chosen L\*a\*b\* colors, with various parametric factors `kL`, `kC` and `kH`.

```
CIEDE2000 Verification Summary :
          Compliance : [ ] CANONICAL [X] SIMPLIFIED
  First Checked Line : -0.0,8.0,32.0,0.0,32.00003,-128.0,1.0,1.0,1.0,52.957588884756206
           Precision : 12 decimal digits
           Successes : 100000000
               Error : 0
            Duration : 330.95 seconds
     Average Delta E : 67.13
   Average Deviation : 5.6e-15
   Maximum Deviation : 3.1e-13
```

```
CIEDE2000 Verification Summary :
          Compliance : [X] CANONICAL [ ] SIMPLIFIED
  First Checked Line : -0.0,8.0,32.0,0.0,32.00003,-128.0,1.0,1.0,1.0,52.9573962651037
           Precision : 12 decimal digits
           Successes : 100000000
               Error : 0
            Duration : 332.23 seconds
     Average Delta E : 67.13
   Average Deviation : 6e-15
   Maximum Deviation : 3.1e-13
```

## Public Domain Licence

You are free to use these files, even for commercial purposes.
