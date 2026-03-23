# Hostile-Cows

Step 1: Sort stalls

Positions must be sorted to place cows greedily.

Step 2: Binary Search on Answer

Minimum distance = 0

Maximum distance = max(stall) - min(stall)

Step 3: Check feasibility

For a given distance d:

Place first cow at first stall

Place next cow at the next stall ≥ last_position + d

Count cows placed

If ≥ k → possible

n, k = map(int, input().split())
stalls = list(map(int, input().split()))

stalls.sort()

def can_place(dist):
    count = 1
    last = stalls[0]

    for i in range(1, n):
        if stalls[i] - last >= dist:
            count += 1
            last = stalls[i]
            if count >= k:
                return True

    return False


low = 0
high = stalls[-1] - stalls[0]
ans = 0

while low <= high:
    mid = (low + high) // 2

    if can_place(mid):
        ans = mid
        low = mid + 1   # try bigger distance
    else:
        high = mid - 1  # reduce distance

print(ans)
