---
layout: post
title: Linux Magic System Request Key [Magic SysRq]
date: 2022-10-05 18:05
author: theguler
comments: true
categories: [Linux / Unix]
---
<!-- wp:image {"id":10882,"width":"191px","height":"auto","sizeSlug":"large","linkDestination":"none"} -->
<figure class="wp-block-image size-large is-resized"><img src="https://theguler.wordpress.com/wp-content/uploads/2024/02/linus-torvalds.webp?w=625" alt="" class="wp-image-10882" style="width:191px;height:auto" /><figcaption class="wp-element-caption"><mark style="background-color:rgba(0, 0, 0, 0);color:#cf2e2e" class="has-inline-color">The Father!</mark></figcaption></figure>
<!-- /wp:image -->

<!-- wp:paragraph -->
<p><strong>What is the magic SysRq key?</strong></p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>It is a 'magical' key combo you can hit which the kernel will respond to regardless of whatever else it is doing, unless it is completely locked up</p>
<!-- /wp:paragraph -->

<!-- wp:list -->
<ul><!-- wp:list-item -->
<li>0 – disable sysrq completely</li>
<!-- /wp:list-item -->

<!-- wp:list-item -->
<li>1 – enable all functions of sysrq</li>
<!-- /wp:list-item -->

<!-- wp:list-item -->
<li>&gt;1 – bitmask of allowed sysrq functions (see below for detailed function description):</li>
<!-- /wp:list-item --></ul>
<!-- /wp:list -->

<!-- wp:preformatted -->
<pre class="wp-block-preformatted"><strong> 2 =   0x2</strong> - enable control of console logging level<br><strong>  4 =   0x4</strong> - enable control of keyboard (SAK, unraw)<br>  <strong>8 =   0x8</strong> - enable debugging dumps of processes etc.<br><strong> 16 =  0x10</strong> - enable sync command<br><strong> 32 =  0x20</strong> - enable remount read-only<br><strong> 64 =  0x40</strong> - enable signalling of processes (term, kill, oom-kill)<br><strong>128 =  0x80</strong> - allow reboot/poweroff<br><strong>256 = 0x100</strong> - allow nicing of all RT tasks</pre>
<!-- /wp:preformatted -->

<!-- wp:paragraph -->
<p><strong>How to set?</strong></p>
<!-- /wp:paragraph -->

<!-- wp:preformatted -->
<pre class="wp-block-preformatted"><strong>##Status</strong><br>cat /proc/sys/kernel/sysrq<br><br><strong>#Fast Temporary Edit:</strong><br>echo "number" &gt;/proc/sys/kernel/sysrq<br><br><strong>#Permanent Edit:</strong><br>sudo nano /etc/sysctl.conf<br><br><strong>#Enable:</strong><br>kernel.sysrq = 1<br><br><strong>#Disable:</strong><br>kernel.sysrq = 0<br><br><strong>#OR:</strong><br>kernel.sysrq = xxx<br><br><strong>#Apply Changes:</strong><br>sudo sysctl -p</pre>
<!-- /wp:preformatted -->

<!-- wp:paragraph -->
<p><strong>How to use?</strong></p>
<!-- /wp:paragraph -->

<!-- wp:list -->
<ul><!-- wp:list-item -->
<li>You press the key Combine: <kbd>ALT+SysRq+<strong>&lt;command&nbsp;key&gt;</strong></kbd></li>
<!-- /wp:list-item -->

<!-- wp:list-item -->
<li>You press the key Combine: <kbd>ALT+Print Screen+<strong>&lt;command&nbsp;key&gt;</strong></kbd></li>
<!-- /wp:list-item --></ul>
<!-- /wp:list -->

<!-- wp:preformatted -->
<pre class="wp-block-preformatted"><strong>=========== ===================================================================<br>Command	    Function<br>=========== ===================================================================</strong><br><strong>``b``</strong>	    Will immediately reboot the system without syncing or unmounting<br>            your disks.<br><strong>``c``	</strong>    Will perform a system crash and a crashdump will be taken<br>            if configured.<br><strong>``d``</strong>	    Shows all locks that are held.<br><strong>``e``</strong>	    Send a SIGTERM to all processes, except for init.<br><strong>``f``</strong>	    Will call the oom killer to kill a memory hog process, but do not<br>	    panic if nothing can be killed.<br><strong>``g``</strong>	    Used by kgdb (kernel debugger)<br><strong>``h``</strong>	    Will display help (actually any other key than those listed<br>            here will display help. but ``h`` is easy to remember :-)<br><strong>``i``</strong>	    Send a SIGKILL to all processes, except for init.<br><strong>``j``</strong>	    Forcibly "Just thaw it" - filesystems frozen by the FIFREEZE ioctl.<br><strong>``k``</strong>	    Secure Access Key (SAK) Kills all programs on the current virtual<br>            console. NOTE: See important comments below in SAK section.<br><strong>``l``</strong>	    Shows a stack backtrace for all active CPUs.<br><strong>``m``</strong>	    Will dump current memory info to your console.<br><strong>``n``</strong>	    Used to make RT tasks nice-able<br><strong>``o``</strong>	    Will shut your system off (if configured and supported).<br><strong>``p``</strong>	    Will dump the current registers and flags to your console.<br><strong>``q``</strong>	    Will dump per CPU lists of all armed hrtimers (but NOT regular<br>            timer_list timers) and detailed information about all<br>            clockevent devices.<br><strong>``r``</strong>	    Turns off keyboard raw mode and sets it to XLATE.<br><strong>``s``</strong>	    Will attempt to sync all mounted filesystems.<br><strong>``t``</strong>	    Will dump a list of current tasks and their information to your<br>            console.<br><strong>``u``</strong>	    Will attempt to remount all mounted filesystems read-only.<br><strong>``v``</strong>	    Forcefully restores framebuffer console<br><strong>``v``</strong>	    Causes ETM buffer dump [ARM-specific]<br><strong>``w``</strong>	    Dumps tasks that are in uninterruptible (blocked) state.<br><strong>``x``</strong>	    Used by xmon interface on ppc/powerpc platforms.<br>            Show global PMU Registers on sparc64.<br>            Dump all TLB entries on MIPS.<br><strong>``y``</strong>	    Show global CPU Registers [SPARC-64 specific]<br><strong>``z``</strong>	    Dump the ftrace buffer<br><strong>``0``-``9``</strong> Sets the console log level, controlling which kernel messages<br>            will be printed to your console. (``0``, for example would make<br>            it so that only emergency messages like PANICs or OOPSes would<br>            make it to your console.)<br><strong>=========== ===================================================================</strong></pre>
<!-- /wp:preformatted -->

<!-- wp:paragraph -->
<p><strong>Credits:</strong></p>
<!-- /wp:paragraph -->

<!-- wp:list -->
<ul><!-- wp:list-item -->
<li>Written by Mydraal <a href="mailto:vulpyne@vulpyne.net">vulpyne@vulpyne.net</a></li>
<!-- /wp:list-item -->

<!-- wp:list-item -->
<li>Updated by Adam Sulmicki <a href="mailto:adam@cfar.umd.edu">adam@cfar.umd.edu</a></li>
<!-- /wp:list-item -->

<!-- wp:list-item -->
<li>Updated by Jeremy M. Dolan <a href="mailto:jmd@turbogeek.org">jmd@turbogeek.org</a> 2001/01/28 10:15:59</li>
<!-- /wp:list-item -->

<!-- wp:list-item -->
<li>Added to by Crutcher Dunnavant</li>
<!-- /wp:list-item --></ul>
<!-- /wp:list -->
