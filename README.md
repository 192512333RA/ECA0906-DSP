clc;
clear;
close all;

% EXPERIMENT 1: BUTTERWORTH IIR FILTER DESIGN

% DESIGN PARAMETERS
Fs = 8000;
Ap = 1;
As = 40;

% 1. LOW-PASS FILTER DESIGN
fp_lp = 1000;
fs_lp = 1500;

wp_lp = fp_lp/(Fs/2);
ws_lp = fs_lp/(Fs/2);

[N_lp, Wn_lp] = buttord(wp_lp, ws_lp, Ap, As);
[b_lp, a_lp] = butter(N_lp, Wn_lp, 'low');

% 2. HIGH-PASS FILTER DESIGN
fp_hp = 2500;
fs_hp = 1800;

wp_hp = fp_hp/(Fs/2);
ws_hp = fs_hp/(Fs/2);

[N_hp, Wn_hp] = buttord(wp_hp, ws_hp, Ap, As);
[b_hp, a_hp] = butter(N_hp, Wn_hp, 'high');

% 3. DISPLAY RESULTS
fprintf('EXPERIMENT 1: BUTTERWORTH IIR FILTERS\n\n');

fprintf('LOW-PASS FILTER\n');
fprintf('Filter Order: %d\n', N_lp);
fprintf('Cutoff Frequency: %.2f Hz\n', Wn_lp*(Fs/2));
fprintf('Numerator Coefficients:\n');
disp(b_lp);
fprintf('Denominator Coefficients:\n');
disp(a_lp);

fprintf('\nHIGH-PASS FILTER\n');
fprintf('Filter Order: %d\n', N_hp);
fprintf('Cutoff Frequency: %.2f Hz\n', Wn_hp*(Fs/2));
fprintf('Numerator Coefficients:\n');
disp(b_hp);
fprintf('Denominator Coefficients:\n');
disp(a_hp);

% 4. FREQUENCY RESPONSE
[H_lp, f] = freqz(b_lp, a_lp, 1024, Fs);
[H_hp, ~] = freqz(b_hp, a_hp, 1024, Fs);

% 5. PLOT RESPONSES
figure('Name', 'Butterworth IIR Filters');

subplot(2,2,1);
plot(f, 20*log10(max(abs(H_lp),1e-8)), 'b', 'LineWidth', 1.5);
grid on;
title('LPF Magnitude Response');
xlabel('Frequency (Hz)');
ylabel('Magnitude (dB)');
ylim([-80 5]);

subplot(2,2,2);
plot(f, unwrap(angle(H_lp))*180/pi, 'r', 'LineWidth', 1.5);
grid on;
title('LPF Phase Response');
xlabel('Frequency (Hz)');
ylabel('Phase (degrees)');

subplot(2,2,3);
plot(f, 20*log10(max(abs(H_hp),1e-8)), 'b', 'LineWidth', 1.5);
grid on;
title('HPF Magnitude Response');
xlabel('Frequency (Hz)');
ylabel('Magnitude (dB)');
ylim([-80 5]);

subplot(2,2,4);
plot(f, unwrap(angle(H_hp))*180/pi, 'r', 'LineWidth', 1.5);
grid on;
title('HPF Phase Response');
xlabel('Frequency (Hz)');
ylabel('Phase (degrees)');<img width="892" height="758" alt="1ST" src="https://github.com/user-attachments/assets/6b183712-3fb1-408e-b367-7e87575233bb" />
