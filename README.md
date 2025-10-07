```markdown
- [x] POWER
- [x] CLOCK_SYNC
- [ ] ASYNC_BUS
- [x] DMA_ENABLE
- [ ] TRACE
- [x] VPU_ENABLE
- [x] EDITOR_ENABLE
- [x] TEXT_MODE
- [ ] RAY_MODE
```

```bus
D0 8 data
A0 8 address
C0 4 control
F0 4 flags
I0 8 io
V0 8 vpu
```

```vcpu
REG R0..R3=0
REG PC=0, SP=255
FLAG Z=0, N=0
```

```asm
MOV R1, 40
MOV R2, 0
MOV R3, 1
L0:
  ADD R2, R3
  ADD R3, 1
  SUB R1, 1
  JNZ R1, L0
OUT R2
PRINT msg
INPUT buffer, 16
VSET 0xE0, 80
VSET 0xE1, 20
VSET 0xE6, 1
VTRIG
HALT
msg:    .string "Enter value: "
buffer: .space  16
```

```clike
let r1 = 40;
fn main() {
  r2 = 0;
  for (i = 1; i <= r1; i = i + 1) { r2 = r2 + i; }
  out(r2);
  print("Enter value: ");
  let buf[16];
  input(buf, 16);
  vset(0xE0,80); vset(0xE1,20); vset(0xE6,1);
  vtrig();
  halt();
}
```

```clike-editor
let r1 = 40;
fn main() {
  print("Hello\n");
  vset(0xE0,80); vset(0xE1,20); vset(0xE6,1);
  vtrig();
  halt();
}
```

<input type="text" id="user-input" value="12345"> <!-- input_user-input -->

<details>
  <summary>Virtual Files</summary>
  <ul>
    <li><code>/hello.txt</code> (15)</li>
    <li><code>/program.asm</code> (1024)</li>
    <li><code>/dump.bin</code> (32)</li>
  </ul>
</details>

```vpu
PLAYER x=3.5 y=3.5 angle=0.00 fov=1.0471976
RES 80x40
STEP 0.02
MAXDIST 16
```

|  |0|1|2|3|4|5|6|7|8|9|
|--:|--:|--:|--:|--:|--:|--:|--:|--:|--:|
|0|1|1|1|1|1|1|1|1|1|1|
|1|1|0|0|0|0|0|0|0|0|1|
|2|1|0|0|0|0|0|0|0|0|1|
|3|1|0|0|0|0|0|0|0|0|1|
|4|1|0|0|0|1|1|0|0|0|1|
|5|1|0|0|0|1|1|0|0|0|1|
|6|1|0|0|0|0|0|0|0|0|1|
|7|1|0|0|0|0|0|0|0|0|1|
|8|1|0|0|0|0|0|0|0|0|1|
|9|1|1|1|1|1|1|1|1|1|1|

```csv
target,feature,command
linux,base,echo "out=${OUT} frame=${FRAME_PATH}"
linux,trace,printf "pc=%d z=%d n=%d\n" ${PC} ${Z} ${N}
win,base,powershell -NoP -C "Write-Output 'out=${OUT}'"
```

<!-- OUTPUT-BEGIN -->

```txt
Console Output:

Ray/Frame:
```

Artifacts:

<!-- OUTPUT-END -->
