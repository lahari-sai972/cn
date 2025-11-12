def charStuff(flagbyte, escbyte, payload):
    x = payload.replace(escbyte, escbyte * 2)
    y = x.replace(flagbyte, escbyte + flagbyte)
    return flagbyte + y + flagbyte

def charDestuff(flagbyte, escbyte, payload):
    x = payload.replace(escbyte * 2, escbyte)
    y = x.replace(escbyte + flagbyte, flagbyte)
    return y[1:-1]

msg = input('Enter some message: ')
fb = input('Enter flag byte: ')
eb = input('Enter escape byte: ')
print('Original message:', msg)
stf = charStuff(fb, eb, msg)
print('Message after character stuffing:', stf)
dstf = charDestuff(fb, eb, stf)
print('Message after character destuffing:', dstf)

def bitstuff(msg):
    count = 0
    st = ""
    for i in msg:
        if i == '1':
            count += 1
            st += i
            if count == 5:
                st += '0'
                count = 0
        else:
            st += i
            count = 0
    return st

def bDestuff(msg):
    unst = ""
    count = 0
    i = 0
    while i < len(msg):
        if msg[i] == '1':
            count += 1
            unst += msg[i]
            if count == 5:
                i += 1
                count = 0
        else:
            unst += msg[i]
            count = 0
        i += 1
    return unst

msg = input("Enter a binary message (like 01111110): ")
bstuff = bitstuff(msg)
print("Message after bit stuffing:", bstuff)
bdestuff = bDestuff(bstuff)
print("Message after bit destuffing:", bdestuff)
