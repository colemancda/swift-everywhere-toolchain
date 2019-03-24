#!/usr/bin/env ruby

require_relative "Scripts/Common/ADB.rb"
require_relative "Scripts/Common/Tool.rb"
require_relative "Scripts/Common/Checkout.rb"
require_relative "Scripts/Common/NDK.rb"

require_relative "Scripts/Builders/ICUBuilder.rb"
require_relative "Scripts/Builders/SwiftBuilder.rb"
require_relative "Scripts/Builders/FoundationBuilder.rb"
require_relative "Scripts/Builders/DispatchBuilder.rb"
require_relative "Scripts/Builders/CurlBuilder.rb"
require_relative "Scripts/Builders/OpenSSLBuilder.rb"
require_relative "Scripts/Builders/XMLBuilder.rb"
require_relative "Scripts/Builders/LLVMBuilder.rb"
require_relative "Scripts/Builders/CMarkBuilder.rb"
require_relative "Scripts/Builders/ClangBuilder.rb"
require_relative "Scripts/Builders/CompilerRTBuilder.rb"

require_relative "Projects/HelloExeBuilder.rb"
require_relative "Projects/HelloLibBuilder.rb"

# References:
#
# - Using Rake to Automate Tasks: https://www.stuartellis.name/articles/rake/
#

task default: ['usage']

desc "Show more actions for ARMv7a targets (for Developers)."
task :more do
   system "rake -T | grep develop | grep armv7a"
end

desc "Checkout Sources of all Components from Git."
task :checkout do
   Checkout.new().checkout()
end

desc "Verify ADB shell setup."
task :verify do ADB.verify end

namespace :armv7a do

   desc "Build Swift Toolchain."
   task :build do
      tool = Tool.new()
      LLVMBuilder.new().make
      ICUBuilder.new(Arch.armv7a).make
      XMLBuilder.new(Arch.armv7a).make
      OpenSSLBuilder.new(Arch.armv7a).make
      CurlBuilder.new(Arch.armv7a).make
      CMarkBuilder.new(Arch.armv7a).make
      swift = SwiftBuilder.new(Arch.armv7a)
      swift.make
      DispatchBuilder.new(Arch.armv7a).make
      FoundationBuilder.new(Arch.armv7a).make
      puts ""
      tool.print("\"Swift Toolchain for Android\" build is completed.")
      tool.print("It can be found in \"#{swift.installs}\".")
      puts ""
   end

   namespace :project do

      helloExe = HelloExeBuilder.new(Arch.armv7a)
      helloLib = HelloLibBuilder.new(Arch.armv7a)

      desc "Builds Hello-Exe project"
      task :buildExe do helloExe.build end

      desc "Builds Hello-Lib project"
      task :buildLib do helloLib.build end

      desc "Deploy and Run Hello-Exe project on Android"
      task :deployExe do
         helloExe.copyLibs()
         adb = ADB.new(helloExe.libs, helloExe.binary)
         adb.deploy()
         adb.run()
      end

      desc "Deploy and Run Hello-Lib project on Android"
      task :deployLib do
         helloLib.copyLibs()
         adb = ADB.new(helloLib.libs, helloLib.binary)
         adb.deploy()
         adb.run()
      end

      desc "Clean Hello-Exe project."
      task :cleanExe do ADB.new(helloExe.libs, helloExe.binary).clean end

      desc "Clean Hello-Lib project."
      task :cleanLib do ADB.new(helloLib.libs, helloLib.binary).clean end
   end

end

# Pass `SA_DRY_RUN=1 rake ...` for Dry run mode.
namespace :develop do

   namespace :armv7a do
      namespace :configure do
         desc "Configure - ICU"
         task :icu do ICUBuilder.new(Arch.armv7a).configure end

         desc "Configure - Swift"
         task :swift do SwiftBuilder.new(Arch.armv7a).configure end

         desc "Configure - LLVM"
         task :llvm do LLVMBuilder.new().configure end

         desc "Configure - CMark"
         task :cmark do CMarkBuilder.new(Arch.armv7a).configure end

         desc "Configure - libDispatch"
         task :dispatch do DispatchBuilder.new(Arch.armv7a).configure end

         desc "Configure - libFoundation"
         task :foundation do FoundationBuilder.new(Arch.armv7a).configure end

         desc "Configure - libXML"
         task :xml do XMLBuilder.new(Arch.armv7a).configure end

         desc "Configure - OpenSSL"
         task :ssl do OpenSSLBuilder.new(Arch.armv7a).configure end

         desc "Configure - curl"
         task :curl do CurlBuilder.new(Arch.armv7a).configure end
      end

      namespace :build do
         desc "Build - ICU"
         task :icu do ICUBuilder.new(Arch.armv7a).build end

         desc "Build - Swift"
         task :swift do SwiftBuilder.new(Arch.armv7a).build end

         desc "Build - LLVM"
         task :llvm do LLVMBuilder.new().build end

         desc "Build - CMark"
         task :cmark do CMarkBuilder.new(Arch.armv7a).build end

         desc "Build - libDispatch"
         task :dispatch do DispatchBuilder.new(Arch.armv7a).build end

         desc "Build - libFoundation"
         task :foundation do FoundationBuilder.new(Arch.armv7a).build end

         desc "Build - libXML"
         task :xml do XMLBuilder.new(Arch.armv7a).build end

         desc "Build - OpenSSL"
         task :ssl do OpenSSLBuilder.new(Arch.armv7a).build end

         desc "Build - curl"
         task :curl do CurlBuilder.new(Arch.armv7a).build end
      end

      namespace :install do
         desc "Install - ICU"
         task :icu do ICUBuilder.new(Arch.armv7a).install end

         desc "Install - Swift"
         task :swift do SwiftBuilder.new(Arch.armv7a).install end

         desc "Install - LLVM"
         task :llvm do LLVMBuilder.new().install end

         desc "Install - CMark"
         task :cmark do CMarkBuilder.new(Arch.armv7a).install end

         desc "Install - libDispatch"
         task :dispatch do DispatchBuilder.new(Arch.armv7a).install end

         desc "Install - libFoundation"
         task :foundation do FoundationBuilder.new(Arch.armv7a).install end

         desc "Install - libXML"
         task :xml do XMLBuilder.new(Arch.armv7a).install end

         desc "Install - OpenSSL"
         task :ssl do OpenSSLBuilder.new(Arch.armv7a).install end

         desc "Install - curl"
         task :curl do CurlBuilder.new(Arch.armv7a).install end
      end

      namespace :make do
         desc "Configure, Build and Install - ICU"
         task :icu do ICUBuilder.new(Arch.armv7a).make end

         desc "Configure, Build and Install - Swift"
         task :swift do SwiftBuilder.new(Arch.armv7a).make end

         desc "Configure, Build and Install - LLVM"
         task :llvm do LLVMBuilder.new().make end

         desc "Configure, Build and Install - CMark"
         task :cmark do CMarkBuilder.new(Arch.armv7a).make end

         desc "Configure, Build and Install - libDispatch"
         task :dispatch do DispatchBuilder.new(Arch.armv7a).make end

         desc "Configure, Build and Install - libFoundation"
         task :foundation do FoundationBuilder.new(Arch.armv7a).make end

         desc "Configure, Build and Install - libXML"
         task :xml do XMLBuilder.new(Arch.armv7a).make end

         desc "Configure, Build and Install - curl"
         task :curl do CurlBuilder.new(Arch.armv7a).make end

         desc "Configure, Build and Install - OpenSSL"
         task :ssl do OpenSSLBuilder.new(Arch.armv7a).make end
      end

      namespace :clean do
         desc "Clean - ICU."
         task :icu do ICUBuilder.new(Arch.armv7a).clean end

         desc "Clean - Swift."
         task :swift do SwiftBuilder.new(Arch.armv7a).clean end

         desc "Clean - LLVM."
         task :llvm do  LLVMBuilder.new().clean end

         desc "Clean - libDispatch"
         task :dispatch do DispatchBuilder.new(Arch.armv7a).clean end

         desc "Clean - libFoundation"
         task :foundation do FoundationBuilder.new(Arch.armv7a).clean end

         desc "Clean - libXML"
         task :xml do XMLBuilder.new(Arch.armv7a).clean end

         desc "Clean - OpenSSL"
         task :ssl do OpenSSLBuilder.new(Arch.armv7a).clean end

         desc "Clean - curl"
         task :curl do CurlBuilder.new(Arch.armv7a).clean end

         desc "Clean - CMark"
         task :cmark do CMarkBuilder.new(Arch.armv7a).clean end
      end
   end
end

task :usage do

   tool = Tool.new()

   tool.print("\nBuilding Swift Toolchain. Steps:\n", 32)

   tool.print("1. Get Sources and Tools.", 32)
   help = <<EOM
   $ rake checkout
EOM
   tool.print(help, 36)

   tool.print("2. Build all Swift components and Sample projects for armv7a.", 32)
help = <<EOM
   $ rake armv7a:build
   $ rake armv7a:project:buildExe
   $ rake armv7a:project:buildLib
EOM
   tool.print(help, 36)

   tool.print("3. Enable USB Debugging on Android device. Install Android Tools for macOS. Connect Android device and Verify ADB shell setup.", 32)
   help = <<EOM
   $ rake verify

   References:
   - How to Install Android Tools for macOS: https://stackoverflow.com/questions/17901692/set-up-adb-on-mac-os-x
   - How to Enable USB Debugging on Android device: https://developer.android.com/studio/debug/dev-options
EOM
   tool.print(help, 36)

   tool.print("4. Deploy and run Demo projects to Android Device.", 32)
   help = <<EOM
   $ rake armv7a:project:deployExe
   $ rake armv7a:project:deployLib
EOM

   tool.print(help, 36)
   system "rake -T | grep --invert-match develop"
end
