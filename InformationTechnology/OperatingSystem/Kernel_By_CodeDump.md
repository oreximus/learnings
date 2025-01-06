## How a Single Bit Inside Your Processor Shields Your Operating System's Integrity

**source**: https://www.youtube.com/watch?v=H4SDPLiUnv4

- Every computer processor has the specific set of actions that it can perform.
- The set of actions of a computer processor is also known as the instruction set of the CPU.
- If we want to provide the control of the system to one software more than other software
  in the system, we can define it by the some set of special instruction that not all of the
  processors used. Many architectures define that known as `Privilege Instructions`.
- The common approach that it uses to the 1 bit operator register which either hold 1 or 0.
- This register is called the `Mode bit`, when it's value is set to 1, the proccessor is said
  to be running in `Privilege mode`, which means it can execute any instruction in the instruction
  set including the `Privilege instructions`.
- If the register value is set to 0, it means it can not execute the `Privilege instruction`.
- CPU internally uses the combination of logic circuits to decodes the incoming instructions.
- The `mode bit` has little to know effect because they run regardless of the `operational mode`.
- In case of `Privilege instruction`, the value held in the `Mode bit` to determine whether
  the running process is allowed to execute them.
- In this way the Privileged instructions can only be executed if the processor is operating
  in `Privilege Mode`.
