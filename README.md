# synestesia
This code assigns a color (or sound) to each positive integer in a natural way, i.e. using physics.

Input: n

1) Factor n into a product of primes n = p_1^s_1 * ... p_r ^s_r

2) Interpret p_i as (proportional to) the wavelength of a photon, and s_i as the number of photons of the given frequency (f=c/lambda). n is then mapped to an EM power spectrum which is simply spiked at each frequency, and the power at each frequency is proportional to s_i.

The only added input is how we scale the wavelengths. The default implementation maps the wavelength of every prime smoothly into the visible range which is roughly 390nm (800Thz, violet) - 700nm (400Thz, red)

3) To convert this spectrum to the appropriate color of light we use the CIE color matching functions (https://www.cs.rit.edu/~ncs/color/t_spectr.html). This can be implemented in almost any language. I used Mathematica. (https://mathematica.stackexchange.com/questions/57389/convert-spectral-distribution-to-rgb-color/57457#57457).

Output: An RBG color specification.

The same method can be used for sound, in which case we just scale into the audible range of 20Hz - 20kHz.

Motivation & Choices: Importantly, *spectra* of colors and sounds combine additively. Combining natural numbers via multiplication is straightforward when presented in their factored form. To transition to addition, take the logrithm (which is proportional to the number of digits, i.e. the size of the representation of n, i.e. the amount of data required to specify it). Note that 

log(n) = sum_i s_i*log(p_i)

We have to choose whether large primes correspond to high or low frequency light/sound. It feels natural to say that large numbers should correspond to higher energies, and therefore higher frequencies. Thus, we set the frequency of a prime to be f_i = log(p_i).

To make things visible, we set 2 to be red/bass, 2 <-> red <-> 400THz. Denote this constant the *key* K. Define the spectrum to be

spec(n) = K * sum_i s_i*\delta(f - log(p_i))

where \delta is the Dirac delta function.

Uses: This could be used to make a *keyboard whose keys are appropriately colored and labeled by prime numbers*. The output of this instrument would be sound, color, and number.
