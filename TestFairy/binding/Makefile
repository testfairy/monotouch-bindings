BTOUCH=/Developer/MonoTouch/usr/bin/btouch
BTOUCHNATIVE=/Developer/MonoTouch/usr/bin/btouch-native
VERSION=1.4.4

all: bin/classic/TestFairy.iOS.dll bin/unified/TestFairy.iOS.dll

libTestFairy.a:
	curl -L -s -o .sdk.zip "http://app.testfairy.com/ios-sdk/TestFairySDK-${VERSION}.zip"
	unzip -q -o .sdk.zip libTestFairy.a
	-rm -f .sdk.zip

bin/unified/TestFairy.iOS.dll: Makefile ApiDefinition.cs AssemblyInfo.cs libTestFairy.a
	-mkdir -p bin/unified
	$(BTOUCHNATIVE) -x=AssemblyInfo.cs ApiDefinition.cs --link-with=libTestFairy.a,libTestFairy.a --out=$@ --new-style -d=__UNIFIED__

bin/classic/TestFairy.iOS.dll: Makefile ApiDefinition.cs AssemblyInfo.cs libTestFairy.a
	-mkdir -p bin/classic
	$(BTOUCH) -x=AssemblyInfo.cs ApiDefinition.cs --link-with=libTestFairy.a,libTestFairy.a --out=$@ 

clean:
	-rm -rf list ios *.sln *.userprefs TestFairy.iOS.dll *.o libTestFairy.a *.zip *.mdb Resources/ lib/ bin/ obj/
