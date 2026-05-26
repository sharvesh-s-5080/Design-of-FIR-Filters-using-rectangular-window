## EXP 3 B : IIR CHEBYSHEV FITER DESIGN

### AIM: 
 To design an IIR Butterworth filter using bilinear transformation in SCILAB. 

### APPARATUS REQUIRED: 
PC installed with SCILAB. 

### PROGRAM (LPF): 
```python
clc;
clear;
close;

//  INPUTS 
wp = input('Passband digital frequency (radians) = ');
ws = input('Stopband digital frequency (radians) = ');
alphap = input('Passband attenuation (Linear) = ');
alphas = input('Stopband attenuation (Linear) = ');
T = input('Sampling time = ');

//  PREWARPING 
omegap = (2/T)*tan(wp/2);
disp("Prewarped passband frequency omegap = " + string(omegap));

omegas = (2/T)*tan(ws/2);
disp("Prewarped stopband frequency omegas = " + string(omegas));

// RIPPLE FACTOR 
epsilon = sqrt(10^(alphap/10) - 1);
disp("Ripple factor epsilon = " + string(epsilon));

//  FILTER ORDER 
N_exact = acosh( sqrt((10^(alphas/10)-1)/(10^(alphap/10)-1)) )/ acosh(omegas/omegap);

N = ceil(N_exact);
disp("Rounded filter order N = " + string(N));

// NORMALIZED POLES (Ωc = 1) 
beta = (1/N) * asinh(1/epsilon);
pols_norm = [];

for k = 1:N
    
    theta = %pi*(2*k-1)/(2*N);
    
    sigma = -sinh(beta)*sin(theta);
    omega = cosh(beta)*cos(theta);
    
    pol_norm = sigma + %i*omega;
    pols_norm = [pols_norm pol_norm];
end

disp("Normalized poles = ");
disp(pols_norm);

//  NORMALIZED TRANSFER FUNCTION 
s = poly(0,'s');

den_norm = real(poly(pols_norm,'s'));
num_norm = real(prod(-pols_norm));

Hn = num_norm / den_norm;

disp("Normalized Transfer Function Hn(s) (Ωc=1) = ");
disp(Hn);

//  UNNORMALIZED (SCALED) POLES 
omegac = omegap;   // Chebyshev Type-I

pols = omegac * pols_norm;   // scale poles directly

disp("Scaled Analog poles = ");
disp(pols);

//  UNNORMALIZED TRANSFER FUNCTION
den_s = real(poly(pols,'s'));
num_s = real(prod(-pols));

Hs = num_s / den_s;

disp("Unnormalized Analog Transfer Function H(s) = ");
disp(Hs);

//  BILINEAR TRANSFORMATION 
z = poly(0,'z');

Hz = horner(Hs, (2/T)*((z-1)/(z+1)));

disp("Digital Transfer Function H(z) = ");
disp(Hz);

//  FREQUENCY RESPONSE 
HW = frmag(Hz,512);
w = 0:%pi/511:%pi;

plot(w/%pi, abs(HW));
xlabel("Normalized Digital Frequency (×π rad/sample)");
ylabel("Magnitude");
title("Frequency Response of Chebyshev Type-I IIR LPF");

```


### PROGRAM (HPF): 
```python
lc;
close;

// User Inputs
wp = input('Pass band frequency (Radians)= ');  // Passband edge > Stopband edge
ws = input('Stop band frequency (Radians)= ');
alphap = input('Pass band attenuation (dB)= ');
alphas = input('Stop band attenuation (dB)= ');
T = input('Sampling Time= ');

// Pre-warping (Bilinear Transformation)
omegap = (2/T)*tan(wp/2);   // Passband edge (analog)
disp(omegap,'omegap=');
omegas = (2/T)*tan(ws/2);   // Stopband edge (analog)
disp(omegas,'omegas=');

// Order of the HPF
N = acosh(sqrt(((10^(0.1*alphas))-1)/((10^(0.1*alphap))-1))) / acosh(omegap/omegas);
disp(N,'N=');
N = ceil(N);
disp('Round off value of N=',N);

// Cutoff frequency
omegac = omegap / (((10^(0.1*alphap))-1)^(1/(2*N)));
disp('omegac=',omegac);


// Chebyshev Prototype (Normalized LPF)
Epsilon = sqrt((10^(0.1*alphap))-1);
disp('Epsilon=',Epsilon);

[pols, gn] = zpch1(N, Epsilon, 1);   // normalized LPF prototype at 1 rad/s
disp('Gain',gn);
disp('Poles',pols);

s = poly(0,'s');   // Laplace variable
hs = poly(gn,'s','coeff') / real(poly(pols,'s'));
disp('Analog Normalized Chebyshev LPF',hs);


// LPF → HPF Transformation (s -> omegac/s)

sh = horner(hs, omegac/s);
disp('Analog Chebyshev High-Pass Filter',sh);


// Bilinear Transformation: s -> (2/T)*((z-1)/(z+1))
z = poly(0,'z');   // z-domain variable
Hz = horner(sh, (2/T) * ((z-1)/(z+1)));
disp('Digital HPF Transfer function H(Z)=',Hz);

// Frequency Response
HW = frmag(Hz, 512);
w = 0:%pi/511:%pi;

plot(w/%pi, abs(HW));
xlabel('Normalized Digital Frequency ×π rad/sample');
ylabel('Magnitude');
title('Frequency Response of Chebyshev IIR High-Pass Filter');

```


### OUTPUT (LPF) : 

<img width="413" height="591" alt="image" src="https://github.com/user-attachments/assets/695921c0-7cd9-4ea5-999a-7c719036eea5" />
<img width="419" height="455" alt="image" src="https://github.com/user-attachments/assets/185261d5-fa23-4273-b7e0-9fb0e20e9e35" />



### OUTPUT (HPF) : 
<img width="402" height="558" alt="image" src="https://github.com/user-attachments/assets/9a07374f-14f0-489e-94d1-f6d4b9939c94" />

<img width="425" height="453" alt="image" src="https://github.com/user-attachments/assets/4f431c69-8a13-441e-850a-72b5774de5a2" />

### RESULT: 
Thus , the IIR Chebyshev filter was designed successfully using bilinear transformation in SCILAB.

