
CONFIGURATION=Release
LATEST_SDK=$(shell xcodebuild -showsdks | grep iphoneos | sed -e 's/.*iphoneos//g' | tail -n 1)


install: armv7s armv7 i386
	mkdir -p ../install/include/SPDY ../install/lib
	lipo -create build/lib/armv7s/libSPDY.a build/lib/armv7/libSPDY.a build/lib/i386/libSPDY.a -output ../install/lib/libSPDY.a
	cp build/include/SPDY/*.h ../install/include/SPDY/

check-%:
	xcodebuild -configuration Debug -sdk iphonesimulator`echo $@ | sed -e 's/check-//'` clean
	xcodebuild -configuration Debug -sdk iphonesimulator`echo $@ | sed -e 's/check-//'` -target SPDYTests | tee /tmp/test-logs

check: check-$(LATEST_SDK)


i386:
	mkdir -p build/lib/i386
	xcodebuild clean
	xcodebuild -sdk iphonesimulator -arch i386 -configuration Debug install
	cp build/UninstalledProducts/libSPDY.a build/lib/i386/libSPDY.a

armv7s:
	mkdir -p build/lib/armv7s
	xcodebuild clean
	xcodebuild -configuration $(CONFIGURATION) -arch armv7s -sdk iphoneos install
	cp build/UninstalledProducts/libSPDY.a build/lib/armv7s/libSPDY.a

armv7:
	mkdir -p build/lib/armv7
	xcodebuild clean
	xcodebuild -configuration $(CONFIGURATION) -arch armv7 -sdk iphoneos install
	cp build/UninstalledProducts/libSPDY.a build/lib/armv7/libSPDY.a
