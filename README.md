"""
Super Look-and-Say

Quy tắc:
1. B1 = "1"
2. B2 = 1 + look-and-say(B1)
3. B3 = 1 + look-and-say(B1) + look-and-say(B2)
4. Bn = nối tất cả B1->Bn-1 + look-and-say(Bn-1)

Hàm tính ratio giữa các bước và sinh n bước đầu.
"""

def look_and_say(s):
    result = ""
    i = 0
    while i < len(s):
        count = 1
        while i+1 < len(s) and s[i] == s[i+1]:
            i += 1
            count += 1
        result += str(count) + s[i]
        i += 1
    return result

def super_look_and_say(n_steps):
    seqs = ["1"]
    for n in range(1, n_steps):
        las = look_and_say(seqs[-1])
        combined = "".join(seqs) + las
        seqs.append(combined)
    return seqs

def ratios(seqs):
    lengths = [len(s) for s in seqs]
    return [lengths[i+1]/lengths[i] for i in range(len(lengths)-1)]

if __name__ == "__main__":
    n = 10
    seqs = super_look_and_say(n)
    print("Super Look-and-Say steps:")
    for i, s in enumerate(seqs, 1):
        print(f"B{i}: {s}")
    print("\nRatios:")
    print(ratios(seqs))
