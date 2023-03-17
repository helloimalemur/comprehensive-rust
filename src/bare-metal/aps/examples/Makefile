# Copyright 2023 Google LLC
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#      http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.

.PHONY: build qemu_minimal qemu qemu_logger

all: minimal.bin improved.bin logger.bin

build:
	cargo build

minimal.bin: build
	aarch64-linux-gnu-objcopy -O binary target/aarch64-unknown-none/debug/minimal $@
improved.bin: build
	aarch64-linux-gnu-objcopy -O binary target/aarch64-unknown-none/debug/improved $@
logger.bin: build
	aarch64-linux-gnu-objcopy -O binary target/aarch64-unknown-none/debug/logger $@

qemu_minimal: minimal.bin
	qemu-system-aarch64 -machine virt -cpu max -serial mon:stdio -display none -kernel $< -s
qemu: improved.bin
	qemu-system-aarch64 -machine virt -cpu max -serial mon:stdio -display none -kernel $< -s
qemu_logger: logger.bin
	qemu-system-aarch64 -machine virt -cpu max -serial mon:stdio -display none -kernel $< -s

clean:
	cargo clean
	rm -f *.bin