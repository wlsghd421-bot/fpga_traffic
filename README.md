# fpga_traffic — STM32_1 FPGA 실습 ② 신호등 제어

전기전자컴퓨터실험설계2 · 박진홍(2023440049) · 2026-10-19 예비

- 보드: Combo II-DLD-Base (Spartan-7 `xc7s75fgga484-1`), 클록 50 MHz
- 최상위: `traffic` (시뮬레이션 `tb`: `sim/tb_traffic.sv`)
- 소스: `src/` (`second_tick`, `traffic_sequence`, `traffic_lights`, `traffic`), XDC: `constraints/traffic.xdc`

## 결과
| 항목 | 결과 |
|---|---|
| Icarus 시뮬레이션 | `PASS traffic: full cycle, pedestrian blink, flicker, reset` (2,186,000 ps) |
| Vivado 합성·구현·비트스트림 | 성공, Critical Warning 0, Error 0 |
| 타이밍 (50 MHz) | WNS +15.109 ns, 모든 제약 만족 |

파형: `docs/sim_wave.png` (방향 0→3, 방향당 phase 0..c 13단계, 초록 8/4/2/1·빨강 7/b/d/e).
시뮬레이션은 1초를 약 10클록으로 줄였고, 실제 보드에서는 `tick`이 1초마다 발생한다.

## 핀 (`Xilinx_S7_Pin_Map.xlsx`)
clk_50mhz B6, rst_p K4(KEY01), flicker Y1(DIP1). 방향 비트 순서는 [3]=N, [2]=E, [1]=S, [0]=W로 **가정**했으며 보드 시연에서 확인한다. `led_left`는 `led_green`과 같은 신호를 별도 핀에 연결했다.
