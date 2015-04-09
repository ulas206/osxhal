# Introduction #

I got the code to compile, but there are a bunch of missing symbols that are in the code. Here is a list of the undefined symbols:

_ath\_hal\_sysctl\_register_ath\_hal\_sysctl\_unregister
_kfree_kmalloc
_memcmp_memcpy
_memset_printk
_snprintf_udelay
_va\_end_va\_start
_vsnprintf_

If you could write up a function for these(or suggest a darwin alternative), I would much appreciate it!

Additionally, I had to make the following hacks that need to be fixed to get it to compile:

- In the ath\_hal\_getuptime function, I had to comment out the following line:
//return ((jiffies / HZ) **1000) + (jiffies % HZ)** (1000 / HZ);
because HZ and jiffies were undefined. Is this linux specific? I doubt this function is important, but I'd like to get everything working as well as possible!

- In the **ath\_hal\_attach function, I had to comment out the following lines:
> /_FIX THIS!
> if (!try\_module\_get(THIS\_MODULE)) {
> > //printk(KERN\_WARNING "%s: try\_module\_get failed\n",__func__);
> >_ath\_hal\_detach(ah);
> > return NULL;

> }**/
because try\_module\_get (obviously) won't work on Mac OSX. Any ideas what could be substituted here?

- In ah\_os.h I had to make the following two define statements because Darwin doesn't have iomem or GFP\_KERNEL symbols.

#define iomem
#define GFP\_KERNEL 0

What is the proper thing to define each as on Darwin?

... And that's the list for the TODO for the HAL! Please help!