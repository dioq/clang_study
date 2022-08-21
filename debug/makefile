
sign:
	/usr/bin/codesign -f -s - --entitlements entitlements.plist ./debugserver

install:
	scp -P 2222 ./debugserver root@localhost:/usr/bin/
