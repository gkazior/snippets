# Sar

## ksar - nice tool for analisys of performance data

   http://ksar.atomique.net/
   Gui is not very pretty, but the soft is great

## collecting

  sar -o test_p_all.sar 1 10

  sar -o test_p_all.sar 1 10  > /dev/null 2>&1 &

## paging

  sar -B     -f test_p_all.sar

## processors

  sar -P ALL -f test_p_all.sar

  sar -q     -f test_p_all.sar

## swap and memory

  sar -r     -f test_p_all.sar

## devices

  sar -d     -f test_p_all.sar

## network

  sar -n ALL -f test_p_all.sar

  sar -n DEV -f test_p_all.sar


# References

  http://linux.die.net/man/1/sar
