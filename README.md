# Detailed Study Guide to Humes & Agarwal (2026), Pages 3–7

## What this report covers

This report explains the five difficult pages of:

O. Humes and J. Agarwal (2026), *Prospects for detecting surface color heterogeneity on asteroid surfaces from sparse multiband photometric survey data*.

- [arXiv abstract](https://arxiv.org/abs/2605.22353)
- [HTML paper](https://arxiv.org/html/2605.22353v1)
- [Published paper](https://doi.org/10.1051/0004-6361/202659422)

The purpose is not merely to restate the paper.

The purpose is to explain:

1. what scientific question is being asked;
2. what data are real and what data are simulated;
3. how one synthetic asteroid is constructed;
4. how synthetic observations are generated;
5. what the photometric model predicts;
6. what a residual means;
7. how viewing and illumination geometry are represented;
8. why multiple linear regression is used;
9. why Spearman correlation is calculated separately in each band;
10. how the Fisher transformation produces the final significance;
11. how true detections and false positives are defined;
12. what Figures 1–5 and Table 1 demonstrate;
13. what the results imply for a real ZTF–DAMIT project.

This is a learning guide.

The original paper remains the authoritative source.

---

# 1. The entire paper section in one simple story

Imagine that an asteroid has one reddish region.

The asteroid is too small to resolve as a disk in a survey image.

It appears as one point of light.

Nevertheless, it rotates.

Sometimes the reddish region faces Earth.

Sometimes it faces away from Earth.

Sometimes it is illuminated by the Sun.

Sometimes it lies on the night side.

If the region is both visible and illuminated, it changes the asteroid's measured brightness more strongly in one filter than another.

The challenge is that an asteroid's brightness also changes because of:

- its irregular shape;
- its rotation;
- its distance from the Sun;
- its distance from Earth;
- its solar phase angle;
- its changing orientation relative to Earth;
- measurement noise.

Those ordinary effects can be much larger than the colour signal.

The authors therefore first build a model of a uniformly coloured asteroid.

That model predicts the normal brightness at every observation time and in every wavelength band.

They subtract the model prediction from each observation.

The remaining difference is called a residual.

They then ask whether the residuals repeatedly change when the same surface direction is visible and illuminated.

Finally, they ask whether that geometry–residual relationship is significantly different between the two filters.

If the relationship is strong in one filter but weak in the other, the difference may indicate a surface-colour feature.

The five pages test how well this idea works under controlled simulations.

---

# 2. What is real, what is sampled, and what is simulated?

This distinction is essential.

The paper does not apply the test to real measured asteroid photometry in these pages.

Instead, it creates artificial photometry whose truth is completely known.

However, parts of the simulation are based on real Solar System populations.

## 2.1 Information taken from real populations

The orbital sampling is based on objects retrieved through a JPL Horizons database query.

The authors consider three populations:

- near-Earth asteroids, abbreviated NEAs;
- main-belt asteroids, abbreviated MBAs;
- trans-Neptunian objects, abbreviated TNOs.

They restrict the database selection to objects with:

$$
H_{\mathrm{mag}}<15.
$$

Here, $H_{\mathrm{mag}}$ is absolute magnitude.

Absolute magnitude is a standardized measure of intrinsic optical brightness.

It is not the brightness measured at one arbitrary distance.

The restriction selects comparatively bright objects.

The sampled real orbits supply realistic distributions of orbital elements.

Examples of orbital elements include:

- semi-major axis;
- eccentricity;
- inclination;
- longitude of ascending node;
- argument of perihelion;
- mean anomaly or equivalent epoch information.

The authors aim to sample the actual orbital distribution of each population.

This gives realistic Sun–object–Earth geometries.

## 2.2 Information created artificially

The following properties are simulated rather than measured for a particular real object:

- detailed asteroid shape;
- spin-axis orientation;
- rotation period;
- initial rotation angle;
- wavelength-dependent phase-function parameters;
- surface spot location;
- spot angular size;
- spot reflectance enhancement;
- simulated observation times;
- simulated magnitudes;
- artificial measurement noise;
- artificial errors in assumed model parameters.

## 2.3 Why combine real orbits with artificial physical properties?

Entirely random orbits could create unrealistic observing geometries.

Entirely real asteroids would not have perfectly known colour maps.

The mixed strategy provides both advantages:

- realistic orbital geometry;
- perfectly known surface truth.

This lets the researchers measure whether their test succeeds.

---

# 3. The three layers of each experiment

Every simulation should be understood as three separate layers.

## Layer A: truth model

The truth model is the artificial asteroid used to generate the observations.

Its exact properties are known to the researchers.

For example, they know the true:

- shape;
- period;
- pole;
- phase function;
- surface reflectance map;
- spot location;
- spot size;
- spot contrast.

## Layer B: synthetic observations

The truth model is observed at artificial survey times.

The forward photometric calculation returns magnitudes.

These magnitudes play the role of telescope measurements.

They may subsequently receive artificial Gaussian noise.

## Layer C: fitted or perturbed test model

The observations are analysed using a model that assumes uniform surface colour.

For sensitivity experiments, one parameter of this analysis model is deliberately perturbed away from its true value.

Examples include:

- an incorrect rotation period;
- an incorrect pole orientation;
- an incorrect shape parameter;
- an incorrect phase-function parameter;
- measurement noise.

The paper then measures how often the colour test still works.

This is analogous to an examination in which the answer is known to the examiner but hidden from the algorithm.

---

# 4. Key vocabulary

## 4.1 Photometry

Photometry means measuring brightness.

## 4.2 Bandpass

A bandpass is a selected wavelength range passed by a filter.

The demonstration uses two bands denoted $V$ and $R$.

A real ZTF application would normally use $g$ and $r$.

## 4.3 Magnitude

Magnitude is a logarithmic representation of brightness.

Smaller magnitude means brighter.

The magnitude difference corresponding to two fluxes is:

$$
m_1-m_2=-2.5\log_{10}\left(\frac{F_1}{F_2}\right).
$$

If an object's flux doubles, its magnitude changes by:

$$
-2.5\log_{10}(2)\approx-0.753\ \mathrm{mag}.
$$

Thus, greater flux produces a more negative magnitude change.

## 4.4 Light curve

A light curve is brightness or magnitude plotted as a function of time or rotational phase.

## 4.5 Surface heterogeneity

Surface heterogeneity means that the surface does not have identical photometric properties everywhere.

## 4.6 Surface-colour heterogeneity

Surface-colour heterogeneity means that the wavelength dependence of reflectance changes across the surface.

A region can therefore be relatively brighter in one band than another.

## 4.7 Null hypothesis

The null hypothesis is that the asteroid is spatially uniform in colour.

It can have an average colour.

The null hypothesis only says that the average colour is the same everywhere on its surface.

## 4.8 Residual

A residual is the difference between an observation and a model prediction.

Using the convention adopted in this guide:

$$
\Delta m_B(t)=m_{B,\mathrm{observed}}(t)-m_{B,\mathrm{model}}(t).
$$

The scientific conclusions do not depend on whether software uses this convention or its negative, provided it is consistent.

## 4.9 Ephemeris

An ephemeris gives the position and observing geometry of an object at specified times.

## 4.10 Detection rate

Detection rate is the fraction of spotted simulations correctly classified as containing a spot.

It is also called the true-positive rate or sensitivity.

## 4.11 False-positive rate

False-positive rate is the fraction of uniform simulations incorrectly classified as containing a spot.

---

# 5. Geometry of an asteroid observation

For every observation time $t$, the simulation needs two important vectors.

Let:

$$
\mathbf E(t)
$$

be the vector from the asteroid towards the observer.

Let:

$$
\mathbf E_0(t)
$$

be the vector from the asteroid towards the Sun.

Their unit vectors are:

$$
\hat{\mathbf E}(t)=\frac{\mathbf E(t)}{|\mathbf E(t)|}
$$

and:

$$
\hat{\mathbf E}_0(t)=\frac{\mathbf E_0(t)}{|\mathbf E_0(t)|}.
$$

The hat symbol means unit vector.

A unit vector has length one and represents direction only.

The length of $\mathbf E$ is the geocentric distance:

$$
\delta=|\mathbf E|.
$$

The length of $\mathbf E_0$ is the heliocentric distance:

$$
r=|\mathbf E_0|.
$$

## 5.1 Why distance matters

Sunlight reaching the asteroid weakens approximately as $1/r^2$.

Reflected light reaching the observer weakens approximately as $1/\delta^2$.

The received flux therefore contains a factor proportional to:

$$
\frac{1}{r^2\delta^2}.
$$

## 5.2 Reduced magnitude

To remove distance variation, asteroid observations are often reduced to unit heliocentric and observer distance.

A common correction is:

$$
m_{\mathrm{red}}=m-5\log_{10}(r\delta).
$$

This does not remove phase, shape, or rotation effects.

It only removes the inverse-square distance scaling.

## 5.3 Light-time correction

The observation timestamp records when photons arrive at the telescope.

The relevant asteroid orientation is the orientation when the photons left the asteroid.

The approximate emission time is:

$$
t_{\mathrm{emit}}=t_{\mathrm{receive}}-\frac{\delta}{c}.
$$

Here, $c$ is the speed of light.

For a main-belt object, the correction can be tens of minutes.

If the asteroid rotates in hours, ignoring this correction can produce a large rotational-phase error.

---

# 6. Why the vectors are transformed into a rotating frame

Ephemeris vectors are initially expressed in ecliptic coordinates.

Ecliptic coordinates are fixed relative to the Solar System reference frame.

The coloured spot is fixed to the asteroid.

Therefore, the Sun and observer vectors must be transformed into an asteroid-fixed rotating frame.

The required rotational state contains:

- pole longitude;
- pole latitude;
- rotation period;
- initial rotation angle;
- reference epoch.

The rotation angle at time $t$ is approximately:

$$
\theta(t)=\theta_0+\frac{2\pi}{P}(t-t_0).
$$

The angle is normally reduced modulo $2\pi$.

The pole direction determines the tilt of the rotating frame.

The period determines how rapidly longitude changes.

The initial angle and reference epoch determine which longitude faces a chosen direction at a known time.

Symbolically, the coordinate transformation can be written:

$$
\hat{\mathbf E}_{\mathrm{body}}(t)
=
\mathbf R(t)\hat{\mathbf E}_{\mathrm{ecl}}(t),
$$

$$
\hat{\mathbf E}_{0,\mathrm{body}}(t)
=
\mathbf R(t)\hat{\mathbf E}_{0,\mathrm{ecl}}(t).
$$

$\mathbf R(t)$ is a rotation matrix constructed from the pole and rotational phase.

In the body frame, a permanent spot stays at a fixed direction.

That is why observations taken years apart can be related to the same physical surface location.

---

# 7. Average viewing and illumination direction

A surface element affects reflected light only when it is both illuminated and visible.

Using the Sun direction alone ignores visibility.

Using the observer direction alone ignores illumination.

The authors obtain better detection rates using an average of the two unit directions:

$$
\bar{\hat{\mathbf E}}
=
\frac{1}{2}
\left(
\hat{\mathbf E}_0+
\hat{\mathbf E}
\right).
$$

This vector is not always a unit vector after averaging.

Its direction points between the illumination and viewing directions.

Its length contains information about their separation.

## 7.1 Relation to phase angle

Let $\alpha$ be the solar phase angle between the two unit vectors.

Then:

$$
\hat{\mathbf E}_0\cdot\hat{\mathbf E}=\cos\alpha.
$$

The squared length of the average is:

$$
\left|\bar{\hat{\mathbf E}}\right|^2
=
\frac{1}{4}
\left|
\hat{\mathbf E}_0+
\hat{\mathbf E}
\right|^2.
$$

Expanding the dot product gives:

$$
\left|\bar{\hat{\mathbf E}}\right|^2
=
\frac{1}{4}
\left(
1+1+2\cos\alpha
\right).
$$

Therefore:

$$
\left|\bar{\hat{\mathbf E}}\right|
=
\cos\left(\frac{\alpha}{2}\right)
$$

for ordinary phase angles between $0$ and $\pi$.

At small phase angle, Sun and observer directions are similar.

The average vector is long.

At large phase angle, the two directions are separated.

The average vector becomes shorter.

For NEAs, the directions can differ by tens of degrees.

That is why considering both is particularly important for NEAs.

## 7.2 Simple example

Suppose:

$$
\hat{\mathbf E}_0=(1,0,0)
$$

and:

$$
\hat{\mathbf E}=(0.8,0.6,0).
$$

Then:

$$
\bar{\hat{\mathbf E}}
=
\frac{1}{2}(1.8,0.6,0)
=
(0.9,0.3,0).
$$

This roughly indicates the surface direction best placed between direct illumination and direct viewing.

---

# 8. The convex triangular shape model

The simulated asteroid is represented by a triangular mesh.

The paper uses 2,000 triangular faces.

Each face has:

- three vertices;
- an area;
- an outward normal;
- a reflectance factor;
- a position on the body.

For vertices $\mathbf v_1$, $\mathbf v_2$, and $\mathbf v_3$, define:

$$
\mathbf a=\mathbf v_2-\mathbf v_1,
$$

$$
\mathbf b=\mathbf v_3-\mathbf v_1.
$$

The unnormalized normal is:

$$
\mathbf N=\mathbf a\times\mathbf b.
$$

The facet area is:

$$
A=\frac{1}{2}|\mathbf N|.
$$

The outward unit normal is:

$$
\hat{\mathbf n}=\frac{\mathbf N}{|\mathbf N|}.
$$

## 8.1 Illumination test

The incidence cosine is:

$$
\mu_0=\hat{\mathbf n}\cdot\hat{\mathbf E}_0.
$$

If $\mu_0\leq0$, the facet lies on the night side.

## 8.2 Visibility test

The exitance cosine is:

$$
\mu=\hat{\mathbf n}\cdot\hat{\mathbf E}.
$$

If $\mu\leq0$, the facet faces away from the observer.

## 8.3 Why convexity helps

For a convex mesh, a facet satisfying both positive dot products can generally be treated as illuminated and visible.

Deep cavities and overhangs are absent.

Full ray tracing for self-shadowing and self-occlusion is therefore unnecessary.

## 8.4 Disk function

The disk function is written:

$$
S(\mu_0,\mu).
$$

It describes how reflected flux changes with incidence and exitance angles.

A generic facet contribution in band $B$ has the structure:

$$
F_{i,B}
\propto
A_iR_{i,B}S(\mu_{0,i},\mu_i).
$$

Only facets with both $\mu_{0,i}>0$ and $\mu_i>0$ contribute.

The total disk-integrated flux is:

$$
F_B(t)=
\sum_{i\in\mathrm{visible,illuminated}}
A_iR_{i,B}S(\mu_{0,i},\mu_i).
$$

The flux is converted to magnitude using:

$$
m_B=C_B-2.5\log_{10}F_B.
$$

---

# 9. Cellinoid shape parameterization

The paper approximates each synthetic body using a Cellinoid-like asymmetric ellipsoid.

The unequal semi-axes are:

$$
a_1,a_2,b_1,b_2,c_1,c_2.
$$

The $c$ axes are aligned with the rotational pole.

The longest axis is fixed as:

$$
a_1=1.
$$

This establishes a relative size scale.

The remaining five axes are drawn from a uniform range approximately between $0.33$ and $1$.

The semiaxes are ordered so that the rotational axis is associated with the shortest dimension.

That arrangement is physically consistent with stable principal-axis rotation.

## 9.1 Why use six semiaxes instead of three?

A standard ellipsoid has three semiaxes $a$, $b$, and $c$.

A Cellinoid permits positive and negative directions along an axis to have different lengths.

This makes the body asymmetric.

The two sides of the asteroid do not have to be mirror images.

Consequently, its rotational light curve can be more realistic than a perfectly symmetric ellipsoid.

## 9.2 Why not use real DAMIT shapes in this population experiment?

The purpose is controlled sensitivity testing across many randomized asteroids.

A parameterized shape provides:

- rapid generation;
- controlled distributions;
- moderate computational cost;
- known truth;
- easy perturbation of one parameter at a time.

Your later real-data project differs because it may use existing DAMIT shape models for selected objects.

---

# 10. Band-dependent photometric inputs

For each band $B$, the model needs three kinds of information.

## 10.1 Absolute magnitude $H_{0,B}$

$H_{0,B}$ sets the brightness scale in band $B$ under an idealized reference geometry.

It is allowed to differ between bands.

The difference between band magnitudes represents mean colour.

The authors set the simulated $H_{0,B}$ values to zero for convenience because absolute scale does not affect this statistical experiment.

They nevertheless allow the fitted values to vary when testing model uncertainty.

## 10.2 Phase function $f_B(\alpha)$

The phase function describes average brightness as a function of solar phase angle $\alpha$.

It can be different in each wavelength band.

The authors use the $HG_{12}^{*}$ system with slope parameter $G_{12}^{*}$.

For each band, $G_{12}^{*}$ is sampled uniformly between 0 and 1.

## 10.3 Reflectance map

The reflectance map assigns a relative reflectance to every facet.

For the background surface, the reflectance factor is effectively one.

For a spot in the affected band, selected facets receive an enhancement $R_f$.

The spot is therefore brighter than its surroundings in that band.

---

# 11. Construction of the artificial surface spot

The red patch shown in Figure 2 is a spherical-cap-like region on the model surface.

Its centre has a latitude and longitude:

$$
(\varphi_{\mathrm{spot}},\theta_{\mathrm{spot}}).
$$

Its angular size is represented by:

$$
\phi_{\mathrm{spot}}.
$$

Be careful not to confuse latitude $\varphi$ with angular spot size $\phi$.

## 11.1 Spot centre

The spot centre is sampled uniformly over the sphere.

Uniform sampling over a sphere does not mean choosing latitude uniformly from $-90^\circ$ to $90^\circ$.

That would overpopulate the poles.

A correct method samples longitude uniformly and samples $\sin\varphi$ uniformly between $-1$ and $1$.

## 11.2 Spot size

The spot angular size is sampled uniformly between:

$$
20^\circ\leq\phi_{\mathrm{spot}}\leq90^\circ.
$$

This represents large regional variations rather than tiny rocks or craters.

Disk-integrated photometry averages light over much of a hemisphere.

Very small regions are therefore strongly diluted.

## 11.3 Spot reflectance

The reflectance enhancement is sampled between:

$$
1.2\leq R_f\leq2.0.
$$

$R_f=1.2$ means 20% greater reflectance than the background in the affected band.

$R_f=2.0$ means twice the background reflectance.

## 11.4 Assigning facets to the spot

Let $\hat{\mathbf q}$ point towards the spot centre.

Let $\hat{\mathbf c}_i$ point towards the centre of facet $i$.

Their angular separation is:

$$
\gamma_i=\cos^{-1}
\left(
\hat{\mathbf c}_i\cdot\hat{\mathbf q}
\right).
$$

The facet belongs to the spot when:

$$
\gamma_i\leq\phi_{\mathrm{spot}}.
$$

Its reflectance is then multiplied by $R_f$ in the affected band.

## 11.5 Why only one band contains the spot

Band 1 is kept uniform.

Band 2 contains the enhanced-reflectance spot.

This creates a clean wavelength-dependent signal.

The simulation is not claiming that real geology affects exactly one filter only.

It is a controlled test of detectability.

---

# 12. Synthetic observing schedule

The paper generates observations across:

$$
3000\ \mathrm{days}.
$$

That is approximately:

$$
\frac{3000}{365.25}\approx8.21\ \mathrm{years}.
$$

For the baseline experiment, the authors choose:

$$
300\ \mathrm{dates\ per\ wavelength\ band}.
$$

With two bands, that gives approximately 600 observations for one synthetic dataset.

The observations in the two bands are sampled at different times.

This imitates non-contemporaneous sparse survey photometry.

## 12.1 Solar elongation restriction

Dates are retained only when solar elongation exceeds:

$$
45^\circ.
$$

Solar elongation is the apparent angular separation between the Sun and the object as seen from Earth.

Ground-based nighttime surveys cannot normally observe an asteroid arbitrarily close to the Sun.

This condition prevents the simulated schedule from including many unrealistic observations.

## 12.2 Orbit propagation

The `kete` package propagates the sampled orbits to each observation time.

It provides the geometry needed to obtain:

- $r$;
- $\delta$;
- $\mathbf E$;
- $\mathbf E_0$;
- solar elongation;
- related ephemeris quantities.

## 12.3 Rotation periods

Rotation periods are sampled uniformly between:

$$
0.1\leq P\leq2\ \mathrm{days}.
$$

In hours, this is:

$$
2.4\leq P\leq48\ \mathrm{hours}.
$$

The lower bound approximately avoids bodies beyond the ordinary spin barrier.

The upper bound avoids ultra-slow rotators, which are more likely to have complex tumbling states.

## 12.4 Initial rotational phase

The initial rotation angle is sampled uniformly between:

$$
0^\circ\leq\theta_0<360^\circ.
$$

This prevents every artificial asteroid from presenting the same face at the reference epoch.

## 12.5 Pole orientation

The rotational pole is sampled uniformly over a sphere.

This produces many inclinations between the spin axis and the orbital or viewing geometry.

---

# 13. From one model asteroid to two datasets

For each selected set of physical properties, two versions of the photometry are generated.

## 13.1 Uniform dataset

Every facet has uniform relative colour.

This dataset represents the null hypothesis.

## 13.2 Spotted dataset

The same orbit, shape, rotation, schedule, and ordinary photometric parameters are used.

One band contains the enhanced-reflectance spot.

This dataset represents the alternative hypothesis.

Using paired versions is scientifically useful.

Differences in performance can be attributed to the spot rather than to a different orbit or schedule.

For 1,000 base synthetic asteroids, this gives:

$$
1000\ \mathrm{spotted}+1000\ \mathrm{uniform}=2000\ \mathrm{datasets}.
$$

---

# 14. The uniform-colour photometric model

The analysis model deliberately assumes that there is no spatial colour variation.

The shape and rotation are wavelength invariant.

Band-specific quantities such as absolute magnitude and phase function may differ.

This is the null model.

The observed magnitude at time $t$ in band $B$ is compared with:

$$
m_B(t),
$$

the model prediction under uniform surface colour.

The residual is:

$$
\Delta m_B(t)=m_{B,\mathrm{obs}}(t)-m_B(t).
$$

For a correct uniform asteroid model, residuals should scatter around zero without a repeatable dependence on body-fixed geometry.

For a spotted asteroid, the uniform model cannot reproduce the extra band-specific brightness whenever the spot contributes.

That produces structured residuals.

---

# 15. Why a nonzero residual alone is not enough

A large residual can arise from:

- random measurement noise;
- a bad observation;
- an incorrect phase function;
- an incorrect period;
- an incorrect pole;
- an incorrect shape;
- a calibration offset;
- an actual surface feature.

Therefore, the test does not simply count large residuals.

It asks whether residuals are systematically related to a fixed direction on the rotating asteroid.

A random error can occur at any orientation.

A permanent spot should affect observations repeatedly when the associated surface region is favourably visible and illuminated.

---

# 16. Multiple linear regression

The average geometry vector has three components:

$$
\bar{\hat{\mathbf E}}
=
(\bar{\hat E}_x,\bar{\hat E}_y,\bar{\hat E}_z).
$$

The surface feature is not guaranteed to align with the $x$, $y$, or $z$ axis.

Checking three separate correlations could miss an oblique direction.

The authors therefore fit:

$$
\Delta m
=
k_x\bar{\hat E}_x
+k_y\bar{\hat E}_y
+k_z\bar{\hat E}_z.
$$

In matrix form:

$$
\mathbf y=\mathbf X\mathbf k+\boldsymbol\epsilon.
$$

Here:

- $\mathbf y$ contains all residuals;
- $\mathbf X$ contains the three geometry components;
- $\mathbf k=(k_x,k_y,k_z)^T$ contains fitted coefficients;
- $\boldsymbol\epsilon$ contains unexplained residual error.

For ordinary least squares, the formal solution is:

$$
\hat{\mathbf k}
=
(\mathbf X^T\mathbf X)^{-1}\mathbf X^T\mathbf y,
$$

when the inverse exists and the design matrix has suitable rank.

The paper implements the regression using `scikit-learn`.

## 16.1 Direction of maximum variation

Normalize the coefficient vector:

$$
\hat{\mathbf k}
=
\frac{(k_x,k_y,k_z)}
{\sqrt{k_x^2+k_y^2+k_z^2}}.
$$

This unit vector points along the body-frame direction where the uniform model's residual varies most strongly.

It is a statistical estimate of the direction associated with the suspected heterogeneity.

It is not automatically a precise surface map.

## 16.2 Projection into one predictor

For each observation, compute:

$$
\mathcal L(\bar{\hat{\mathbf E}})
=
\bar{\hat{\mathbf E}}\cdot\hat{\mathbf k}.
$$

Expanded:

$$
\mathcal L
=
\bar{\hat E}_x\hat k_x
+\bar{\hat E}_y\hat k_y
+\bar{\hat E}_z\hat k_z.
$$

$\mathcal L$ is the projection of the observing geometry along the direction of maximum residual variation.

It compresses a three-dimensional geometry into one scalar.

When $\mathcal L$ is large and positive, the average geometry points broadly along $\hat{\mathbf k}$.

When it is negative, it points broadly opposite $\hat{\mathbf k}$.

When it is near zero, the geometry is roughly perpendicular to that direction or weakly projected onto it.

---

# 17. A numerical regression example

Suppose three observations have average geometry vectors:

$$
\bar{\hat{\mathbf E}}_1=(0.8,0.1,0.0),
$$

$$
\bar{\hat{\mathbf E}}_2=(0.2,0.7,0.1),
$$

$$
\bar{\hat{\mathbf E}}_3=(-0.7,0.0,0.2).
$$

Suppose regression finds:

$$
\mathbf k=(-0.9,0.1,0.2).
$$

Its norm is:

$$
|\mathbf k|
=
\sqrt{(-0.9)^2+0.1^2+0.2^2}
=
\sqrt{0.86}
\approx0.927.
$$

Therefore:

$$
\hat{\mathbf k}
\approx
(-0.971,0.108,0.216).
$$

For the first observation:

$$
\mathcal L_1
=
(0.8)(-0.971)+(0.1)(0.108)+(0)(0.216)
\approx-0.766.
$$

The same calculation produces one predictor for every observation.

The algorithm can now correlate residual with a single geometry coordinate.

---

# 18. Why all bands are used in the regression

The paper combines photometry from all bands when finding $\hat{\mathbf k}$.

This identifies the direction that maximizes residual variation in the complete dataset.

After fixing that common direction, correlations are evaluated separately for each band.

This matters because using a different direction for every band could make each band look artificially well correlated.

A common direction gives a fairer comparison.

For rigorous real-data validation, the fact that the same data help select the direction and test correlations should be examined through simulation, resampling, or held-out validation.

The paper calibrates performance through its Monte Carlo experiments.

---

# 19. Spearman rank correlation

For each band $B$, the authors calculate the Spearman rank correlation:

$$
\rho_B
=
\operatorname{corr}_{\mathrm{Spearman}}
\left[
\mathcal L(\bar{\hat{\mathbf E}}),
\Delta m_B
\right].
$$

Spearman correlation measures whether two quantities have a monotonic relationship.

It uses ranks instead of the raw numerical values.

## 19.1 Meaning of $\rho$

$$
\rho\approx+1
$$

means residual generally increases as $\mathcal L$ increases.

$$
\rho\approx-1
$$

means residual generally decreases as $\mathcal L$ increases.

$$
\rho\approx0
$$

means there is little monotonic association.

## 19.2 Why Spearman instead of Pearson?

Pearson correlation mainly measures linear association in raw values.

Spearman is sensitive to a monotonic trend even when the exact relationship is curved.

It is also less dominated by extreme raw values.

The residual response of a partially visible spot need not be perfectly linear.

## 19.3 Small rank example

Suppose increasing values of $\mathcal L$ have ranks:

$$
1,2,3,4,5.
$$

Suppose residual ranks are:

$$
1,2,4,3,5.
$$

The ordering is very similar, so Spearman correlation is strongly positive.

---

# 20. Why compare correlations between bands?

An inaccurate wavelength-independent shape can produce geometry-related residuals in both bands.

A colour feature should affect the two bands differently.

Therefore, the central signal is not merely a large $|\rho_B|$.

It is a statistically significant difference between:

$$
\rho_{B_1}
$$

and:

$$
\rho_{B_2}.
$$

Example of a possible shape-model problem:

$$
\rho_g=-0.65,
\qquad
\rho_r=-0.62.
$$

Both bands behave similarly.

Example of a possible colour-dependent feature:

$$
\rho_g=-0.05,
\qquad
\rho_r=-0.68.
$$

The association is much stronger in one band.

---

# 21. Fisher transformation

A raw correlation coefficient is bounded between $-1$ and $1$.

Its sampling distribution is not normally distributed, especially near the boundaries.

The Fisher transformation is:

$$
z_B
=
\frac{1}{2}
\ln
\left(
\frac{1+\rho_B}{1-\rho_B}
\right).
\tag{2}
$$

This is equivalent to:

$$
z_B=\operatorname{atanh}(\rho_B).
$$

The transformed quantity is more nearly normally distributed for suitable sample sizes.

## 21.1 Numerical examples

If:

$$
\rho=0,
$$

then:

$$
z=0.
$$

If:

$$
\rho=0.5,
$$

then:

$$
z
=
\frac{1}{2}\ln(3)
\approx0.5493.
$$

If:

$$
\rho=-0.5,
$$

then:

$$
z\approx-0.5493.
$$

---

# 22. Significance of the difference between two bands

For bands $B_1$ and $B_2$, the paper calculates:

$$
z_{B_1,B_2}
=
\frac{z_{B_1}-z_{B_2}}
{\sqrt{
\frac{1}{n_{B_1}-3}
+
\frac{1}{n_{B_2}-3}
}}.
\tag{1}
$$

Here:

- $z_{B_1}$ is the Fisher-transformed correlation in band 1;
- $z_{B_2}$ is the Fisher-transformed correlation in band 2;
- $n_{B_1}$ is the number of observations in band 1;
- $n_{B_2}$ is the number of observations in band 2.

The denominator is the standard error for the difference under the assumption of independent samples.

The $-3$ terms arise from the approximate variance of a Fisher-transformed correlation:

$$
\operatorname{Var}(z)\approx\frac{1}{n-3}.
$$

For two independent correlations, variances add:

$$
\operatorname{Var}(z_1-z_2)
\approx
\frac{1}{n_1-3}+
\frac{1}{n_2-3}.
$$

Taking the square root gives the denominator in Equation 1.

---

# 23. Worked Fisher-significance example

Suppose:

$$
\rho_V=-0.10,
$$

$$
\rho_R=-0.60,
$$

and:

$$
n_V=n_R=100.
$$

Transform the $V$-band correlation:

$$
z_V
=
\frac12\ln\left(\frac{1-0.10}{1+0.10}\right)
\approx-0.1003.
$$

Transform the $R$-band correlation:

$$
z_R
=
\frac12\ln\left(\frac{1-0.60}{1+0.60}\right)
\approx-0.6931.
$$

The difference is:

$$
z_V-z_R
\approx0.5928.
$$

The standard error is:

$$
\sqrt{\frac1{97}+\frac1{97}}
\approx0.1436.
$$

Therefore:

$$
z_{V,R}
\approx
\frac{0.5928}{0.1436}
\approx4.13.
$$

This example does not pass the paper's $5\sigma$ threshold.

If the correlations were more different or the sample larger, the score would increase.

---

# 24. Meaning and limitation of the independence assumption

Equation 1 assumes the two correlations come from independent samples.

The paper treats the bands as independent because observations in the two bands occur at different times.

This is appropriate for non-contemporaneous sparse survey measurements under their setup.

If both bands were measured simultaneously at every epoch, their errors and brightness variations could be paired.

Then a direct colour curve could be analysed instead.

That is closer to the approach used in targeted studies such as Lacerda's work on Haumea.

For real survey data, one must check whether exposure timing, calibration, repeated nights, and shared systematics undermine strict independence.

---

# 25. The $5\sigma$ decision threshold

The paper identifies a candidate when:

$$
z_{B_1,B_2}>5.
$$

This is called a $5\sigma$ threshold.

Under an ideal standard normal distribution, a one-sided value beyond 5 is extremely rare.

However, the practical false-positive rate must still be tested empirically because:

- the direction $\hat{\mathbf k}$ is fitted from data;
- the data may not be perfectly Gaussian;
- parameter errors can create structure;
- many asteroids or hypotheses may be tested;
- real surveys have systematic errors.

That is why the uniform synthetic datasets are essential.

---

# 26. Monte Carlo sensitivity experiment

Monte Carlo analysis means repeating an experiment many times with randomly drawn inputs.

For each base synthetic asteroid, the authors create multiple perturbed analysis models.

The paper states that 73 perturbed models are generated for each synthetic asteroid, differing from the truth in one parameter at a time.

For a parameter $q$ with true value $q_{\mathrm{true}}$, a typical perturbation is:

$$
q_{\mathrm{assumed}}
\sim
\mathcal N
\left(
q_{\mathrm{true}},\sigma_q^2
\right).
$$

$\sigma_q$ is varied.

Small $\sigma_q$ means accurate model knowledge.

Large $\sigma_q$ means inaccurate model knowledge.

For every perturbation level, the complete colour test is rerun.

The authors then calculate:

$$
\mathrm{Detection\ rate}
=
\frac{N(\mathrm{spotted\ datasets\ detected})}
{N(\mathrm{spotted\ datasets})},
$$

and:

$$
\mathrm{False\ positive\ rate}
=
\frac{N(\mathrm{uniform\ datasets\ detected})}
{N(\mathrm{uniform\ datasets})}.
$$

---

# 27. Figure 1: the complete test, panel by panel

![Pages 3–4 containing the test and Figure 1](figures/page_4.png)

Figure 1 uses one simulated asteroid with a high-albedo feature in the $R$ band.

## 27.1 Top panel: magnitude versus time

The horizontal axis is Julian Date.

The vertical axis is magnitude.

Black points represent simulated $V$-band observations.

Red points represent simulated $R$-band observations.

The continuous curves represent fitted uniform-colour models.

The repeated oscillation is primarily the rotational light curve produced by shape.

The $R$-band surface feature creates additional departures from the uniform model.

## 27.2 Why the curves repeat

The body is elongated and asymmetric.

Its projected area changes as it rotates.

Broadside orientations tend to be brighter.

Narrow-side orientations tend to be fainter.

## 27.3 Second panel: residual versus time

The model is subtracted from the simulated observation.

Black residuals remain relatively near zero.

Red residuals contain conspicuous negative excursions.

Under the guide's residual convention, negative magnitude residual means brighter than predicted.

The high-reflectance $R$-band spot causes that behaviour.

## 27.4 Why time alone is insufficient

The deviations occur at multiple dates.

Time is not a fixed surface coordinate.

The asteroid's orbital and rotational geometry must be calculated to determine whether those dates correspond to the same physical region.

## 27.5 Third row: residual against geometry components

Residuals are plotted separately against:

$$
\bar{\hat E}_x,
\qquad
\bar{\hat E}_y,
\qquad
\bar{\hat E}_z.
$$

The red residuals show structure with geometry.

The black residuals are less strongly structured.

No single coordinate is guaranteed to align with the surface feature.

## 27.6 Bottom panel: residual against $\mathcal L$

Multiple regression finds $\hat{\mathbf k}$.

Each geometry vector is projected onto that direction.

The horizontal axis becomes:

$$
\mathcal L(\bar{\hat{\mathbf E}}).
$$

The red residuals now show a clear monotonic trend.

The black residuals do not show the same strong trend.

## 27.7 Final step not drawn

The authors calculate $\rho_V$ and $\rho_R$.

They apply Equations 1 and 2.

The resulting significance determines whether the difference between bands exceeds $5\sigma$.

## 27.8 What Figure 1 proves and does not prove

It demonstrates the algorithm on a clear simulated example.

It does not establish performance for every asteroid.

Population-level performance is evaluated in later figures.

---

# 28. Figure 2: synthetic asteroid parameterization

![Page 5 containing Figure 2 and Table 1](figures/page_5.png)

Figure 2 is a geometric diagram of the Cellinoid and surface spot.

The axes $a_i$, $b_i$, and $c_i$ describe unequal semiaxes.

The $c$ direction is the rotational pole direction.

The red area is the enhanced-reflectance spot.

Its centre is described by longitude and latitude.

Its angular extent is $\phi_{\mathrm{spot}}$.

The cone in the diagram shows the angular boundary of the patch as seen from the body's centre.

Every facet whose centre falls within the cone receives the enhanced reflectance in the affected band.

The diagram is a parameterization, not an image of a real asteroid.

---

# 29. Table 1: effect of population and spot size

Table 1 reports detection rate for NEAs, MBAs, and TNOs in bins of spot angular size.

The values are:

| Spot-size interval | NEAs | MBAs | TNOs |
|---|---:|---:|---:|
| $80^\circ<\phi_{\mathrm{spot}}\leq90^\circ$ | 1.00 | 1.00 | 0.99 |
| $70^\circ<\phi_{\mathrm{spot}}\leq80^\circ$ | 1.00 | 1.00 | 0.98 |
| $60^\circ<\phi_{\mathrm{spot}}\leq70^\circ$ | 1.00 | 1.00 | 0.96 |
| $50^\circ<\phi_{\mathrm{spot}}\leq60^\circ$ | 1.00 | 1.00 | 0.93 |
| $40^\circ<\phi_{\mathrm{spot}}\leq50^\circ$ | 0.99 | 1.00 | 0.92 |
| $30^\circ<\phi_{\mathrm{spot}}\leq40^\circ$ | 0.99 | 0.99 | 0.85 |
| $20^\circ<\phi_{\mathrm{spot}}\leq30^\circ$ | 0.91 | 0.96 | 0.74 |

## 29.1 How to read 0.91

A value of 0.91 means 91% of spotted simulations in that subgroup passed the detection criterion.

It does not mean that an individual candidate has a 91% probability of being real.

Population detection rate and individual posterior probability are different concepts.

## 29.2 Main trend

Larger spots are easier to detect.

Their reflectance difference contributes a larger fraction of disk-integrated flux.

## 29.3 Why TNO rates are lower

The paper explains that the simulated 3,000-day survey covers different fractions of the orbital timescale for the three populations.

NEAs and MBAs experience broader changes in geometry during the survey.

TNOs move slowly through their long orbits.

Only a limited range of seasons, subsolar latitudes, and longitudes may be sampled.

A spot outside the well-sampled visible and illuminated region can therefore be missed.

## 29.4 Why the authors restrict later analysis

Because TNO and NEA performance depends strongly on specific geometry and orbital sampling, subsequent parameter-sensitivity analysis is restricted mainly to the MBA subpopulation.

MBAs better isolate the parameter being perturbed under the simulated survey duration.

---

# 30. Seasonal versus rotational sampling

Two different timescales matter.

## 30.1 Rotational timescale

This is hours to days.

It changes which longitude faces the observer.

## 30.2 Orbital or seasonal timescale

This is months to centuries depending on the population.

It changes the subsolar and sub-observer latitudes and the accessible illumination geometry.

A survey can sample many rotations yet still poorly sample seasonal geometry.

For a distant TNO, eight years may cover only a small fraction of one orbit.

This distinction explains why merely increasing observation count does not guarantee complete surface coverage.

---

# 31. Figure 3: effect of total observation count

![Page 6 containing Figure 3](figures/page_6.png)

Figure 3 has two panels.

Both plot detection rate on the vertical axis.

The horizontal axis is total number of observations.

The two bands have equal observation counts in this experiment.

Therefore, 100 total observations means approximately 50 observations per band.

## 31.1 Top panel: curves separated by spot size

Dark red curves represent larger spots.

Lighter red curves represent smaller spots.

The black curve represents uniform asteroids and therefore the false-positive behaviour.

Detection rate rises rapidly as the number of observations increases.

Large spots approach high detection rate with fewer observations.

Small spots require more observations.

## 31.2 Bottom panel: curves separated by reflectance enhancement

Dark curves represent stronger enhancements closer to $R_f=2$.

Light curves represent weaker enhancements closer to $R_f=1.2$.

Stronger spots are easier to detect.

Weak-contrast spots require larger samples.

## 31.3 The approximately 100–150 observation result

The paper reports that detection rate reaches approximately 1 for all modeled spot sizes and reflectance enhancements with roughly 100–150 observations in total under the idealized assumptions.

That corresponds to roughly 50–75 observations per band when sampling is balanced.

This is not a universal real-data guarantee.

It assumes:

- the rest of the model is correct;
- noise conditions match the experiment;
- sampled geometries are adequate;
- the feature lies in the simulated range;
- observations are distributed according to the simulation.

## 31.4 False-positive curve

The black no-spot curve stays close to zero.

This means the $5\sigma$ threshold rarely identifies a feature in ideal uniform simulations.

---

# 32. Why fewer observations reduce detection

There are two related reasons.

First, a small sample may not observe the spot often enough when it is visible and illuminated.

Second, the uncertainty of a correlation coefficient is larger for small $n$.

From Equation 1, the standard-error terms are:

$$
\frac{1}{n_B-3}.
$$

As $n_B$ increases, these terms decrease.

Therefore, the same difference between correlations produces a larger significance when supported by more observations.

---

# 33. Figure 4: unequal numbers of observations in the two bands

![Page 7 containing Figure 4 and Figure 5](figures/page_7.png)

Figure 4 contains two heatmaps.

Rows give the number of observations in Band 1.

Columns give the number of observations in Band 2.

Band 1 is uniform.

Band 2 contains the spot.

The top heatmap is detection rate.

The bottom heatmap is false-positive rate.

## 33.1 Selected detection-rate examples

With 10 observations in each band, the detection rate is 0.27.

With 10 in Band 1 and 30 in Band 2, it rises to 0.80.

With 30 in Band 1 and 30 in Band 2, it is 0.90.

With 50 in Band 1 and 50 in Band 2, it is 0.96.

With 125 in each band, it is 0.99.

## 33.2 Why Band 2 count matters especially strongly

Band 2 contains the surface feature.

More Band 2 observations provide more chances to sample the feature and define its geometry-related residual trend.

## 33.3 Why too few Band 1 observations are still a problem

The test compares two correlations.

If Band 1 has very few points, its correlation estimate is noisy.

The fitted geometry direction may also be influenced disproportionately by the better-sampled spotted band.

## 33.4 The asymmetric false-positive pattern

False positives increase when one band has many observations and the other has very few.

Examples from the heatmap include values near 0.10–0.12 in the most strongly imbalanced corners.

When both bands have moderate and comparable sample sizes, false-positive rates are approximately zero in this experiment.

## 33.5 Why imbalance can create false positives

The well-sampled band can map the shape-related residual variation much more completely than the poorly sampled band.

The two measured correlations may then differ because of sampling quality rather than colour.

Equation 1 accounts for sample size in its nominal standard error, but severely different geometry coverage can still create practical problems.

## 33.6 Practical lesson

Do not select targets using total observation count alone.

Check:

- observations in $g$;
- observations in $r$;
- ratio of the two counts;
- rotational-phase coverage;
- phase-angle coverage;
- subsolar-coordinate coverage;
- sub-observer-coordinate coverage;
- apparition coverage.

---

# 34. Figure 5: sensitivity to random Gaussian noise

Figure 5 also has two panels.

The horizontal axis is the standard deviation of added magnitude noise.

The vertical axis is detection rate.

The black no-spot curve represents false-positive behaviour.

## 34.1 Artificial noise model

For a noiseless simulated magnitude $m_{\mathrm{true}}$, the noisy observation is:

$$
m_{\mathrm{obs}}
=
m_{\mathrm{true}}+\epsilon,
$$

where:

$$
\epsilon\sim\mathcal N(0,\sigma_m^2).
$$

$\sigma_m$ is expressed in magnitudes.

## 34.2 What noise does to residuals

Noise increases vertical scatter in $\Delta m_B$.

It is not systematically tied to $\bar{\hat{\mathbf E}}$.

Therefore, it weakens a real geometry–residual correlation.

It does not normally create a stable geometry dependence by itself.

## 34.3 Top panel: spot-size dependence

Large spots remain detectable at higher noise than small spots.

Small spots, especially those around $20^\circ$–$30^\circ$, lose detectability quickly.

The paper notes that for errors above about 0.1 mag, detection of the smallest modeled spots falls below roughly 50%.

## 34.4 Bottom panel: reflectance dependence

High-$R_f$ spots remain detectable at greater noise.

Low-contrast spots with $R_f<1.2$ would be strongly affected even by relatively modest noise; the simulated lower range around 1.2 therefore represents a practical boundary.

## 34.5 Why false positives remain low

Independent Gaussian noise reduces correlation rather than creating a coherent direction-dependent signal.

The no-spot curve consequently remains near zero.

## 34.6 Important real-world warning

Real photometric errors are not always independent Gaussian noise.

Survey data can contain:

- night-dependent zero-point errors;
- colour terms;
- filter-dependent calibration errors;
- saturation;
- trailing losses;
- blending with stars;
- seeing-dependent biases;
- background-subtraction errors;
- outliers;
- correlated errors within an exposure sequence.

Such systematic errors may behave differently from Figure 5.

Injection and recovery on actual survey sampling is therefore necessary.

---

# 35. Why magnitude noise of 0.1 is substantial

A magnitude difference $\Delta m$ corresponds to flux ratio:

$$
\frac{F_2}{F_1}=10^{-0.4\Delta m}.
$$

For $\Delta m=0.1$:

$$
10^{-0.04}\approx0.912.
$$

Thus, 0.1 mag corresponds to roughly a 9% flux difference in one direction.

This is large enough to obscure weak disk-integrated colour signals.

---

# 36. Understanding the most important causal chain

The simulation establishes this chain:

$$
\text{surface spot}
\rightarrow
\text{band-dependent facet flux}
\rightarrow
\text{band-dependent integrated magnitude}
\rightarrow
\text{structured model residual}
\rightarrow
\text{correlation with body-frame geometry}
\rightarrow
\text{different correlations between bands}
\rightarrow
z_{B_1,B_2}.
$$

If any link is broken, the test may fail.

Examples:

- if the spot is never visible, it does not change integrated flux;
- if the contrast is too weak, noise dominates;
- if the period is wrong, the inferred longitude is wrong;
- if one band is poorly sampled, the correlation comparison is unstable;
- if the shape model is poor, residuals may contain unrelated geometry structure.

---

# 37. One complete worked toy experiment

Consider one simulated MBA.

Assume:

$$
P=8\ \mathrm{hours}.
$$

Assume the spot radius is:

$$
\phi_{\mathrm{spot}}=40^\circ.
$$

Assume the affected band has:

$$
R_f=1.5.
$$

Assume 75 observations are taken in $V$ and 75 in $R$.

## Step 1: generate ephemerides

For each time, calculate $r$, $\delta$, $\mathbf E$, and $\mathbf E_0$.

Reject epochs with solar elongation below $45^\circ$.

## Step 2: calculate asteroid orientation

Light-time correct every epoch.

Use the pole, period, initial phase, and reference epoch to calculate the body orientation.

## Step 3: calculate flux

Transform Sun and observer directions into the body frame.

For every facet, calculate $\mu_0$ and $\mu$.

Add the reflected flux from facets that are both illuminated and visible.

Apply the relevant phase function and distance scaling.

Convert flux to magnitude.

## Step 4: create the two datasets

Create a uniform version.

Create a spotted version with enhanced $R$-band reflectance in the selected facets.

## Step 5: fit uniform photometric models

Analyse each dataset under a model that assumes no spatial colour variation.

## Step 6: calculate residuals

Suppose the uniform dataset gives residuals near zero in both bands.

Suppose the spotted dataset gives ordinary $V$ residuals but negative $R$ residuals when the spot contributes.

## Step 7: construct average geometry

For each observation:

$$
\bar{\hat{\mathbf E}}
=
\frac12
(\hat{\mathbf E}_0+\hat{\mathbf E}).
$$

## Step 8: fit regression

Use all residuals and geometry components to obtain $\hat{\mathbf k}$.

## Step 9: calculate scalar predictor

For every observation:

$$
\mathcal L
=
\bar{\hat{\mathbf E}}\cdot\hat{\mathbf k}.
$$

## Step 10: calculate band correlations

Suppose:

$$
\rho_V=-0.08,
$$

$$
\rho_R=-0.75.
$$

## Step 11: transform and compare

Calculate $z_V$, $z_R$, and $z_{V,R}$.

## Step 12: classify

If:

$$
z_{V,R}>5,
$$

the spotted simulation is counted as detected.

If the same happens for the uniform simulation, it is counted as a false positive.

---

# 38. What Figure 3 does not mean

Figure 3 does not mean every real asteroid needs exactly 100 observations.

It does not mean 100 observations guarantee detection.

It does not mean observations may have arbitrary errors.

It does not mean total count is more important than filter balance.

It does not mean tiny surface features are detectable.

It reports performance inside one controlled simulated population and parameter range.

---

# 39. What Figure 4 does not mean

The heatmap values are not probabilities that one real candidate is heterogeneous.

They are empirical rates over simulated populations.

The axes count observations, not nights.

Many points taken under almost identical geometry may provide less information than the same number spread across useful geometries.

---

# 40. What Figure 5 does not mean

The added Gaussian standard deviation is not a complete model of ZTF uncertainty.

Real uncertainties can be heteroscedastic, meaning each observation has a different error bar.

They can also be correlated or systematically biased.

The figure isolates one simple effect: independent random magnitude scatter.

---

# 41. Relationship between spot size, contrast, count, and noise

These four quantities trade against one another.

A large, high-contrast spot creates a strong signal.

It can be detected with fewer or noisier measurements.

A small, low-contrast spot creates a weak signal.

It needs more accurate measurements and better geometry coverage.

Conceptually, detectability grows with something like:

$$
\mathrm{effective\ signal}
\sim
\frac{
\mathrm{visible\ spot\ fraction}
\times
\mathrm{contrast}
\times
\sqrt{N_{\mathrm{effective}}}
}
{\sigma_m},
$$

but this is an explanatory scaling, not the exact test statistic used by the paper.

$N_{\mathrm{effective}}$ is smaller than raw observation count when many observations repeat nearly identical geometry.

---

# 42. A symbol dictionary

| Symbol | Meaning |
|---|---|
| $t$ | Observation epoch |
| $B$ | Photometric bandpass |
| $B_1,B_2$ | The two compared bands |
| $m_B(t)$ | Predicted magnitude in band $B$ at time $t$ |
| $m_{B,\mathrm{obs}}(t)$ | Observed or synthetic measured magnitude |
| $\Delta m_B(t)$ | Observation–model residual |
| $H_{0,B}$ | Band-dependent absolute-magnitude normalization |
| $f_B(\alpha)$ | Band-dependent phase function |
| $\alpha$ | Solar phase angle |
| $r$ | Heliocentric distance |
| $\delta$ | Observer or geocentric distance |
| $\mathbf E$ | Asteroid-to-observer vector |
| $\mathbf E_0$ | Asteroid-to-Sun vector |
| $\hat{\mathbf E}$ | Observer unit direction |
| $\hat{\mathbf E}_0$ | Sun unit direction |
| $\bar{\hat{\mathbf E}}$ | Average illumination and viewing vector |
| $\bar{\hat E}_x,\bar{\hat E}_y,\bar{\hat E}_z$ | Components in rotating body coordinates |
| $\mathbf k$ | Multiple-regression coefficient vector |
| $\hat{\mathbf k}$ | Unit direction of maximum residual variation |
| $\mathcal L(\bar{\hat{\mathbf E}})$ | Projection of geometry along $\hat{\mathbf k}$ |
| $\rho_B$ | Spearman correlation in band $B$ |
| $z_B$ | Fisher transformation of $\rho_B$ |
| $z_{B_1,B_2}$ | Significance of the difference between band correlations |
| $n_B$ | Number of observations in band $B$ |
| $P$ | Rotational period |
| $\theta_0$ | Initial rotation angle |
| $t_0$ | Reference epoch |
| $\mu_0$ | Cosine of incidence angle |
| $\mu$ | Cosine of exitance angle |
| $S(\mu_0,\mu)$ | Disk or scattering function |
| $A_i$ | Area of facet $i$ |
| $\hat{\mathbf n}_i$ | Outward normal of facet $i$ |
| $R_{i,B}$ | Reflectance factor of facet $i$ in band $B$ |
| $R_f$ | Reflectance enhancement inside the spot |
| $\varphi_{\mathrm{spot}}$ | Spot latitude |
| $\theta_{\mathrm{spot}}$ | Spot longitude |
| $\phi_{\mathrm{spot}}$ | Angular size or radius parameter of spot |
| $\sigma_m$ | Standard deviation of added magnitude noise |

---

# 43. What is being fitted and what is being held fixed?

The exact answer depends on the particular sensitivity experiment.

The general strategy is to perturb one item while keeping the rest at truth.

This is called a one-factor-at-a-time sensitivity analysis.

It answers questions such as:

- How accurate must the period be if everything else is correct?
- How much random magnitude noise can be tolerated if the geometry model is correct?
- How damaging is a pole error if the period and shape are correct?

It does not automatically describe the fully realistic case where all errors occur simultaneously.

That will generally be harder.

---

# 44. Direct problem versus inverse problem

The direct or forward problem is:

$$
\text{known shape, spin, geometry, and reflectance}
\rightarrow
\text{predicted brightness}.
$$

The inverse problem is:

$$
\text{measured brightness}
\rightarrow
\text{estimated shape, spin, phase function, or surface property}.
$$

The paper uses the direct problem to generate synthetic observations.

It then applies a statistical inverse inference to ask whether surface colour is heterogeneous.

DAMIT models themselves were generally produced by earlier inverse light-curve modelling.

`lcgenerator` then uses those recovered models in the forward direction.

---

# 45. Relevance to a ZTF–DAMIT implementation

The simulation tells you what an ideal pipeline needs.

## 45.1 Real inputs

- ZTF timestamps;
- ZTF $g$ and $r$ magnitudes;
- photometric uncertainties;
- filter identity;
- quality flags;
- asteroid designation;
- ephemerides;
- DAMIT shape;
- DAMIT pole solution;
- DAMIT rotation period;
- reference epoch and phase information;
- a phase-function model.

## 45.2 Required preprocessing

- remove unusable measurements;
- account for light-time;
- calculate heliocentric and observer distances;
- calculate phase angle and solar elongation;
- transform Sun and observer vectors into the body frame;
- ensure units and coordinate conventions match;
- predict shape-and-rotation brightness;
- fit band-dependent magnitude and phase terms;
- compute residuals.

## 45.3 Statistical stage

- calculate $\bar{\hat{\mathbf E}}$ for every epoch;
- combine band residuals for the common regression direction;
- compute $\hat{\mathbf k}$;
- compute $\mathcal L$;
- compute Spearman correlation separately in $g$ and $r$;
- calculate the Fisher difference statistic;
- calibrate significance using injections and null tests.

---

# 46. Essential validation for real data

## 46.1 Uniform synthetic recovery

Run the complete pipeline on uniform simulated asteroids.

Measure the empirical false-positive rate.

## 46.2 Spot injection and recovery

Inject spots with different:

- sizes;
- latitudes;
- longitudes;
- contrasts;
- filter responses.

Use the actual timestamps and uncertainties of each real target.

## 46.3 Period perturbation

Sample plausible periods from the DAMIT uncertainty or alternative solutions.

Repeat the test.

A candidate should not disappear under tiny plausible changes unless that sensitivity is honestly reported.

## 46.4 Pole perturbation

Test all published mirror-pole solutions where applicable.

Perturb within uncertainty.

## 46.5 Shape uncertainty

Test alternative DAMIT models or bootstrap shape solutions if available.

## 46.6 Phase-function uncertainty

Repeat using plausible phase-function parameters and possibly alternative phase-law families.

## 46.7 Filter balance

Downsample the richer band to match the poorer band.

Check whether the candidate remains significant.

## 46.8 Time scrambling

Randomly permute residuals among epochs while keeping the sampling geometry.

This breaks a real surface association and provides an empirical null distribution.

## 46.9 Split-sample validation

Find the candidate direction using one subset of observations.

Test the correlation difference on an independent subset.

This guards against overfitting the direction to noise.

## 46.10 Apparition validation

Fit or discover the signal in one apparition.

Check whether it returns in another apparition when the same body-frame region is sampled.

This is especially convincing for a stable surface feature.

---

# 47. Common misunderstandings

## Misunderstanding 1

“The paper directly sees a spot.”

Correction: the object is unresolved; a geometry-dependent colour signature is inferred statistically.

## Misunderstanding 2

“Any large residual means a spot.”

Correction: residuals must repeat with surface geometry and differ between bands.

## Misunderstanding 3

“The model assumes identical brightness in both bands.”

Correction: absolute magnitude and phase function may differ by band; spatial colour is assumed uniform under the null.

## Misunderstanding 4

“The regression produces the exact spot map.”

Correction: it produces a direction of maximum residual variation, not a high-resolution surface image.

## Misunderstanding 5

“A 5-sigma formula guarantees no false detections.”

Correction: real systematic errors and repeated searches require empirical calibration.

## Misunderstanding 6

“Three hundred observations per band are required.”

Correction: 300 per band is the baseline synthetic schedule; the authors separately study smaller counts.

## Misunderstanding 7

“The population detection rate is the probability that one candidate is genuine.”

Correction: those are different statistical quantities.

## Misunderstanding 8

“A convex model includes realistic crater shadows.”

Correction: it excludes important non-convex self-shadowing and self-occlusion.

---

# 48. Questions to ask while reading each graph

For every graph, ask:

1. What is on the horizontal axis?
2. What is on the vertical axis?
3. What parameter changes between curves?
4. What is held fixed?
5. Does the graph show detection rate, false-positive rate, or an individual residual?
6. Is the dataset uniform or spotted?
7. Is the value a simulated population statistic or an individual-object probability?
8. What assumption makes the result optimistic?
9. What would change with real ZTF uncertainties?
10. What does the graph imply for target selection?

---

# 49. Page-by-page reading map

## Page 3

Main ideas:

- average illumination and viewing vector;
- regression direction;
- projection $\mathcal L$;
- Spearman correlations;
- Fisher transformation;
- $5\sigma$ decision rule;
- full algorithm summary.

## Page 4

Main ideas:

- Figure 1 workflow;
- truth versus perturbed models;
- Monte Carlo design;
- direct photometric model inputs;
- beginning of synthetic population construction.

## Page 5

Main ideas:

- Cellinoid geometry;
- phase and magnitude parameters;
- spot location, size, and reflectance;
- Figure 2;
- Table 1 population detection rates;
- why later analysis emphasizes MBAs.

## Page 6

Main ideas:

- population geometry discussion;
- minimum number of observations;
- Figure 3;
- why small and weak spots need more data;
- importance of seasonal and rotational coverage.

## Page 7

Main ideas:

- unequal filter counts;
- Figure 4 heatmaps;
- random Gaussian magnitude noise;
- Figure 5;
- loss of sensitivity with increasing noise;
- beginning of period-error analysis.

---

# 50. The algorithm as pseudocode

```python
for asteroid in synthetic_population:
    orbit = sampled_realistic_orbit(asteroid.population)
    shape = make_cellinoid_mesh(n_facets=2000)
    spin = sample_pole_period_phase()
    phase_functions = sample_band_phase_functions()
    spot = sample_spot_location_size_contrast()

    times_band1 = sample_visible_epochs(n=300, span_days=3000)
    times_band2 = sample_visible_epochs(n=300, span_days=3000)

    uniform_data = []
    spotted_data = []

    for band, times in [("B1", times_band1), ("B2", times_band2)]:
        for time in times:
            corrected_time = light_time_correct(time)
            sun_vector, observer_vector = ephemeris(corrected_time)
            sun_body, observer_body = rotate_to_body_frame(
                sun_vector, observer_vector, spin
            )

            uniform_mag = integrate_mesh_brightness(
                shape, sun_body, observer_body,
                phase_functions[band], uniform_reflectance
            )

            spotted_mag = integrate_mesh_brightness(
                shape, sun_body, observer_body,
                phase_functions[band], spotted_reflectance_for_band(band)
            )

            uniform_data.append(observation(time, band, uniform_mag))
            spotted_data.append(observation(time, band, spotted_mag))

    for dataset in [uniform_data, spotted_data]:
        model = fit_uniform_colour_model(dataset)
        residuals = observed_minus_predicted(dataset, model)

        average_vectors = []
        for observation in dataset:
            sun_body, observer_body = model_geometry(observation.time)
            average_vectors.append(0.5 * (sun_body + observer_body))

        k = fit_multiple_regression(average_vectors, residuals)
        k_hat = k / norm(k)
        L = [dot(vector, k_hat) for vector in average_vectors]

        rho_band1 = spearman(L_for_band1, residuals_for_band1)
        rho_band2 = spearman(L_for_band2, residuals_for_band2)

        fisher1 = atanh(rho_band1)
        fisher2 = atanh(rho_band2)

        score = (fisher1 - fisher2) / sqrt(
            1 / (n_band1 - 3) + 1 / (n_band2 - 3)
        )

        detected = score > 5
```

This pseudocode communicates the logic.

It omits many implementation details, numerical conventions, uncertainty checks, and the appendix's precise photometric equations.

---

# 51. What you should be able to explain to a professor

You can say:

> The authors first create unresolved two-band light curves for artificial asteroids with known shapes, spins, orbits and surface maps. For every epoch they calculate which part of the rotating asteroid is illuminated and visible. They then fit a model that assumes spatially uniform colour and subtract it from the simulated observations. A real surface feature should leave band-dependent residuals whenever the same body-fixed region contributes to the observed light. Multiple regression finds the surface direction most associated with the residuals, and the three-dimensional geometry is projected onto that direction. The authors calculate a Spearman correlation between this predictor and residual magnitude separately in each band, then use the Fisher transformation to test whether the two correlations differ by more than five standard deviations. Uniform simulations measure false positives, while spotted simulations measure detection efficiency. Figures 3–5 show that performance improves with more balanced observations and decreases with higher noise, smaller spots and weaker reflectance contrast.

---

# 52. The single most important conceptual distinction

The method is not simply comparing average $V-R$ colour.

It is testing whether the colour-related residual changes with a repeatable body-fixed viewing and illumination geometry.

Mean colour asks:

> Is the asteroid globally red or blue?

This method asks:

> Does one part of the asteroid behave differently in colour from another part?

---

# 53. Final summary

The authors build artificial but physically plausible unresolved asteroids.

They sample realistic orbital geometries using real population distributions.

They assign randomized shape, spin, phase and spot properties.

They generate sparse non-simultaneous photometry in two filters.

They create a uniform version and a spotted version for each base asteroid.

They analyse both with a uniform-colour model.

They calculate model residuals.

They associate residuals with the average Sun–surface–observer geometry in the rotating frame.

They use multiple regression to find the direction of maximum residual variation.

They project every geometry onto that direction.

They compute a Spearman correlation separately in each band.

They use the Fisher transformation to compare the two correlations.

They classify scores above $5\sigma$ as candidate detections.

They measure detection rates using spotted simulations.

They measure false-positive rates using uniform simulations.

They find that larger and higher-contrast spots are easier to detect.

They find that balanced filter sampling is important.

They find that independent Gaussian noise mainly destroys true detections rather than creating false ones.

They show that the survey's duration and geometry coverage matter in addition to raw observation count.

For real ZTF work, these results define a starting point, not a completed validation.

The real implementation must additionally propagate DAMIT model uncertainty, ZTF systematics, alternative pole and period solutions, filter imbalance, and target-specific observing geometry.

