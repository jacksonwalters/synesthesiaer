#SYNESTHESIAER
#keyboard which assigns a prime number, a light frequency, and sound frequency
#to keys. it mixes the light frequencies to corresponding RGB colors, mixes
#(eventually) the pure tones to sounds, and multiplies the primes to get unique
#numbers
This code assigns a color and sound to a range of positive integers in a natural
way.

Input: n

1) Factor n into a product of primes n = p_1^s_1 * ... p_r ^s_r

The only added input is how we scale the wavelengths. The default implementation maps the wavelength of every prime smoothly into the visible range which is roughly 380nm (800Thz, violet) - 700nm (400Thz, red)

3) To convert this spectrum to the appropriate color of light we use the CIE color matching functions (https://www.cs.rit.edu/~ncs/color/t_spectr.html). This can be implemented in almost any language. (https://mathematica.stackexchange.com/questions/57389/convert-spectral-distribution-to-rgb-color/57457#57457).

Output: An RBG color specification.

The same method can be used for sound, in which case we just scale into the audible range of 20Hz - 20kHz. We then need to mix the tones to get a sound using a synthesizer package.

Importantly, *spectra* of colors and sounds combine additively. Combining natural numbers via multiplication is straightforward when presented in their factored form. To transition to addition, take the logarithm. Note that

log(n) = sum_i s_i*log(p_i)

We have to choose whether large primes correspond to high or low frequency light/sound. It feels natural to say that large numbers should correspond to higher energies, and therefore higher frequencies. To make things visible, we set some initial prime b to be red/bass, b <-> red <-> 400THz = f_0. We include this as the base for the logarithm. This is akin to selecting a key, i.e. this tells you which prime is red. Thus, we set the frequency of a prime to be

f_b(p) = f_0*log_b(p).

Define the spectrum to be

spec(n) = sum_i s_i*\delta(f - f_b(p_i))

where \delta is the Dirac delta function.

This could be used to make a *keyboard whose keys are appropriately colored and labeled by prime numbers*. The output of this instrument would be sound, colored light, and positive integers. It will then become possible to play a sequence of numbers. The set of primes available for a given base/key would be the primes in the visible/audible range.
