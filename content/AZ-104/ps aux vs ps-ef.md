`ps aux` and `ps -ef` are the same. 

This duality traces back to historical differences between POSIX Unix systems (of which Linux is one) and BSD Unix systems (the most common of which is macOS). 

In the beginning, POSIX used `-ef` while the BSD required `aux`. Today, both operating-system families accept either format.