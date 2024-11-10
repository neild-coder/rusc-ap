CC=gcc
TARGET=application
SRC=application-src/main.c application-src/rust_binder.c
BUILD_DIR=build

RUST_LIB_DEBUG=target/debug/ 
RUST_LIB_RELEASE=target/release/

LOGGING_FLAGS=-DLOGGING=1

GREEN=\033[0;32m
RED=\033[0;31m
NC=\033[0m # No Color

debug:
	@echo "\n${GREEN}Building debug version...${NC}\n"
	
	cargo build 
	$(CC) -o $(TARGET) $(LOGGING_FLAGS) $(SRC) -L$(RUST_LIB_DEBUG) -lrapplication
	
	@echo "\n${GREEN}Building success...${NC}\n"
	@if [ -d build ]; then \
		echo "\n${GREEN}Build directory exists. Moving files to ./build${NC}\n"; \
	else \
		echo "\n${GREEN}Build directory created. Moving files to ./build${NC}\n"; \
		mkdir $(BUILD_DIR); \
	fi
	mv application build/

release:
	@echo "\n${GREEN}Building release version...${NC}\n"
	
	cargo build --release
	$(CC) -o $(TARGET) -Os $(SRC) -L$(RUST_LIB_RELEASE) -lrapplication
	
	@echo "\n${GREEN}Building success...${NC}\n"
	@if [ -d build ]; then \
		echo "\n${GREEN}Build directory exists. Moving files to ./build${NC}\n"; \
	else \
		echo "\n${GREEN}Build directory created. Moving files to ./build${NC}\n"; \
		mkdir $(BUILD_DIR); \
	fi
	mv application $(BUILD_DIR)/

doc:
	cargo doc --no-deps --target-dir=./doc
	zip -r rust_doc.zip doc/doc/

clean:
	cargo clean
	rm -rf doc
	rm -rf rust_doc.zip
	rm -rf $(BUILD_DIR)
