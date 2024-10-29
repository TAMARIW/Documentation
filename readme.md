The fastest way to get started is to flash the backup images inside the Images folder onto the raspberry pi sdcards. For this follow the HowTo Backup and Restore guide.
To setup the pi from scratch, follow the guides in this order:
- Raspberry Pi Setup
- HowTo Setup OpenCV
- HowTo Setup ORPE
- HowTo Setup Datalink

For reference, the TAMARIW Satellite A is often named or refered to as TMWA and B as TMWB.

To get started with the code base used on the STM32, follow the HowTo STM32 guide to setup the project, compile and flash.

It should be noted that the datalink uses a modified version of rodos where the gateway loop time was increased.

I highly recommend creating a fork or another version of the repos containing the code base. This will also require updating the git clone paths inside the guides.
The repos are located at the following links:
- https://gitlab.com/chst15/tamariw/orpetmw
- https://gitlab.com/chst15/tamariw/datalinktmw
- https://gitlab.com/chst15/tamariw/stm32tmw