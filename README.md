# 4-A Design of FIR Filters using Rectangular Window


### AIM:        
  To generate design of FIR digital filter using rectangular window in SCILAB .  

### APPARATUS REQUIRED: 
  PC Installed with SCILAB 

### PROGRAM 
#### a. Design of Low Pass FIR Digital filter
```python
clc;
close;

M = input('Enter the Odd Filter Length = ');
Wc = input('Enter the Digital Cut off frequency = ');

alpha = (M-1)/2; // Center value

for n = 1:M
    if (n == alpha+1) then
        hd(n) = Wc/%pi;
    else
        hd(n) = sin(Wc*((n-1)-alpha))/(((n-1)-alpha)*%pi);
    end
end

// Rectangular Window
for n = 1:M
    W(n) = 1;
end

// Windowing filter coefficients
h = hd .* W;

disp("Filter Coefficients:");
disp(h);

[hzm,fr] = frmag(h,256);

subplot(2,1,1)
plot(2*fr,hzm)
xlabel('Normalized Digital Frequency w');
ylabel('Magnitude');
title('Frequency Response of FIR LPF using Rectangular Window');

hzm_dB = 20*log10(hzm);

subplot(2,1,2)
plot(2*fr,hzm_dB)
xlabel('Normalized Digital Frequency w');
ylabel('Magnitude in dB');
title('Frequency Response of FIR LPF using Rectangular Window');

```
#### b. Design of High Pass FIR Digital filter
```python
clc;
close;

M = input('Enter the Odd Filter Length = ');
Wc = input('Enter the Digital Cut off frequency = ');

alpha = (M-1)/2;

for n = 1:M
    if (n == alpha+1) then
        hd(n) = 1 - (Wc/%pi);
    else
        hd(n) = -sin(Wc*((n-1)-alpha))/(((n-1)-alpha)*%pi);
    end
end

// Rectangular Window
for n = 1:M
    W(n) = 1;
end

h = hd .* W;

disp("Filter Coefficients:");
disp(h);

[hzm,fr] = frmag(h,256);

subplot(2,1,1)
plot(2*fr,hzm)
xlabel('Normalized Digital Frequency w');
ylabel('Magnitude');
title('Frequency Response of FIR HPF using Rectangular Window');

hzm_dB = 20*log10(hzm);

subplot(2,1,2)
plot(2*fr,hzm_dB)
xlabel('Normalized Digital Frequency w');
ylabel('Magnitude in dB');
title('Frequency Response of FIR HPF using Rectangular Window');

```
#### c. Design of Band Pass FIR Digital filter
```python
clc;
close;

M = input('Enter the Odd Filter Length = ');
Wc1 = input('Enter the Lower Cut off frequency = ');
Wc2 = input('Enter the Upper Cut off frequency = ');

alpha = (M-1)/2;

for n = 1:M
    if (n == alpha+1) then
        hd(n) = (Wc2 - Wc1)/%pi;
    else
        hd(n) = (sin(Wc2*((n-1)-alpha)) - sin(Wc1*((n-1)-alpha)))/(((n-1)-alpha)*%pi);
    end
end

// Rectangular Window
for n = 1:M
    W(n) = 1;
end

h = hd .* W;

disp("Filter Coefficients:");
disp(h);

[hzm,fr] = frmag(h,256);

subplot(2,1,1)
plot(2*fr,hzm)
xlabel('Normalized Digital Frequency w');
ylabel('Magnitude');
title('Frequency Response of FIR BPF using Rectangular Window');

hzm_dB = 20*log10(hzm);

subplot(2,1,2)
plot(2*fr,hzm_dB)
xlabel('Normalized Digital Frequency w');
ylabel('Magnitude in dB');
title('Frequency Response of FIR BPF using Rectangular Window');

```
#### d. Design of Band Stop FIR Digital filter
```python
clc ; 
close ; 
M=input('Enter the Odd Filter Length ='); 
Wc1 = input('Enter the Lower Cut off frequency = ');
Wc2 = input('Enter the Upper Cut off frequency = '); 
alpha= (M -1)/2 // Center Value 
for n = 1:M 
    if (n ==alpha+1) 
        hd(n) =1-((Wc2-Wc1)/%pi) ; 
    else 
        hd(n) =((sin(Wc1 *((n -1)-alpha)))-(sin(Wc2 *((n -1)-alpha))))/(((n -1)-alpha)*%pi); 
    end 
end 
// Rectangular Window
 
for n = 1:M 
    W(n) =1; 
end 
//Windowing filter coefficients 

h = hd.*W; 
disp('Filter Coefficients are') 
disp(h) 

[hzm,fr]= frmag (h,256) ; 

subplot(2 ,1 ,1) 
plot(2*fr, hzm) 
xlabel( ' Normalized Digital Frequency w'); 
ylabel( 'Magnitude '); 
title( ' Frequency Response of  FIR BSF using Rectangular Window ') 

hzm_dB = 20* log10 (hzm); 

subplot (2 ,1 ,2); 
plot(2*fr , hzm_dB); 
xlabel( ' Normalized Digital Frequency W' ); 
ylabel( 'Magnitude in dB'); 
title('Frequency Response of FIR BSF using Rectangular Window');

```
### OUTPUT
#### a. Design of Low Pass FIR Digital filter
<img width="384" height="406" alt="image" src="https://github.com/user-attachments/assets/611cb982-5f11-4ce6-8e7a-e34052a47bb2" />

<img width="446" height="414" alt="image" src="https://github.com/user-attachments/assets/40c4fd09-85ee-46e3-a6da-fb1baddd4ca8" />

#### b. Design of High Pass FIR Digital filter

<img width="382" height="416" alt="image" src="https://github.com/user-attachments/assets/f09f4dfe-f284-431c-8d31-4a370f7fa7ef" />

<img width="448" height="422" alt="image" src="https://github.com/user-attachments/assets/cde9c54f-ac8f-4647-88b1-f5d495da939b" />

#### c. Design of Band Pass FIR Digital filter

<img width="380" height="456" alt="image" src="https://github.com/user-attachments/assets/eaa3a8e4-a9c3-4169-bfe2-d7c3e913e5f5" />

<img width="435" height="450" alt="image" src="https://github.com/user-attachments/assets/48449795-d5e8-415f-8b31-0c9991632afc" />

#### d. Design of Band Stop FIR Digital filter

<img width="386" height="467" alt="image" src="https://github.com/user-attachments/assets/325fc06a-72ff-446c-adb2-5b8724b62bf0" />

<img width="443" height="469" alt="image" src="https://github.com/user-attachments/assets/17d205ad-c6d1-4476-9e00-c6a9ab371a1c" />

### RESULT
The FIR Filters were successfully designed using rectangular window Technique.
