.PHONY: all configure build clean full-clean fresh run

# Out-of-source CMake build
BUILD_DIR ?= build
CONFIG ?= Debug
CMAKE ?= cmake

all: build

configure:
	$(CMAKE) -S . -B $(BUILD_DIR) -DCMAKE_BUILD_TYPE=$(CONFIG)

build: configure
	$(CMAKE) --build $(BUILD_DIR) --config $(CONFIG)

run: build
	@exe="$(BUILD_DIR)/glfw_opengl3"; \
	[ -x "$$exe" ] || exe="$(BUILD_DIR)/$(CONFIG)/glfw_opengl3"; \
	[ -x "$$exe" ] || { echo "Executable not found in build directory"; exit 1; }; \
	"$$exe"

clean:
	@if [ -d "$(BUILD_DIR)" ]; then \
		$(CMAKE) --build $(BUILD_DIR) --target clean --config $(CONFIG) || true; \
	fi

full-clean:
	@rm -rf "$(BUILD_DIR)"
	@# Remove leftover root-level objects/executables so we never rely on prebuilt artefacts
	@find . -maxdepth 1 -type f \( -name '*.o' -o -name '*.obj' -o -name 'glfw_opengl3' -o -name 'example_glfw_opengl3' -o -name '*.exe' \) -delete

fresh: full-clean all
