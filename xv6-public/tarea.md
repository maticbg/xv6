Grupo 14
Matías Briones
Moussa Saker
Amparo Diaz
 
Archivos modificados:
cuenta.c
defs.h
Makefile
proc.c
syscall.c
syscall.h
sysproc.c
user.h
usys.S

Codigo agregado:

cuenta.c:

1
#include "types.h"
#include "stat.h"
#include "user.h"
int main(void) {
printf(1, "La cantidad de procesos en ejecucion en la CPU es %d\n",
getprocs());
exit();
}

defs.h:

123
int             getprocs(void);

Makefile:

184
	_cuenta\
		
254
	cuenta.c\

proc.c:

537
int
getprocs(void)
{
  struct proc *p;
  int count = 0;

  acquire(&ptable.lock);

  for(p = ptable.proc; p < &ptable.proc[NPROC]; p++)
  {
     if(p->state != UNUSED)
        count++;
  }

  release(&ptable.lock);

 return count;
}

syscall.c:

106
extern int sys_getprocs(void);

130
[SYS_getprocs] sys_getprocs,

syscall.h:

23
#define SYS_getprocs  22

sysproc.c:

94
int
sys_getprocs(void)
{
  return getprocs();
}

user.h:

26
int getprocs(void);

usys.S:

32
SYSCALL(getprocs)
