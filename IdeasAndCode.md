
Put this in the game loop code: Into the 'loading up the game state' nested loop. It will list the locations of my bots.

```
            if owner == 1 and units:
                where_me_msg += str(j) + ',' + str(i) + '    '
    print(where_me_msg, file=sys.stderr, flush=True)
```

