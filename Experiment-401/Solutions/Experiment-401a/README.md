#include <stdio.h>
#include <stdlib.h>
#include <sys/neutrino.h>
#include <sys/syspage.h>
#include <unistd.h>

int main(int argc, char *argv[])
{
    int irq = 1;           // interrupt number (example: keyboard)
    int id;

    printf("Simple Interrupt Example\n");

    /* Attach interrupt */
    id = InterruptAttach(irq, NULL, NULL, 0, 0);
    if (id == -1)
    {
        perror("InterruptAttach");
        return EXIT_FAILURE;
    }

    printf("Attached to interrupt %d\n", irq);

    while (1)
    {
        /* Wait for interrupt */
        InterruptWait(0, NULL);

        printf("Interrupt received!\n");
    }

    return 0;
}
