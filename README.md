# Vector3_To_IntPtr
Convert Unity Vector3 to Int Ptr
```cs
using System.Numerics;
using System.Runtime.InteropServices;

namespace ConsoleApp1
{
    internal abstract class Program
    {

        [DllImport("Vec3ToPtr.dll", CallingConvention = CallingConvention.Cdecl)]
        private static extern IntPtr GetVector2Address(ref Vector2Custom vector);

        [DllImport("Vec3ToPtr.dll", CallingConvention = CallingConvention.Cdecl)]
        private static extern IntPtr GetVector3Address(ref Vector3Custom vector);

        [DllImport("Vec3ToPtr.dll", CallingConvention = CallingConvention.Cdecl)]
        private static extern IntPtr GetVector4Address(ref Vector4Custom vector);

        [DllImport("Vec3ToPtr.dll", CallingConvention = CallingConvention.Cdecl)]
        private static extern IntPtr GetIntAddress(int intValue);

        [DllImport("Vec3ToPtr.dll", CallingConvention = CallingConvention.Cdecl)]
        private static extern IntPtr GetFloatAddress(float floatValue);

        [DllImport("Vec3ToPtr.dll", CallingConvention = CallingConvention.Cdecl)]
        private static extern IntPtr GetDoubleAddress(double doubleValue);


        private static void Main()
        {
            var vector2 = new Vector2(1, 2);
            var vector2Custom = new Vector2Custom { x = vector2.X, y = vector2.Y };
            IntPtr address = GetVector2Address(ref vector2Custom);
            unsafe
            {
                Console.WriteLine($"X: {*(float*)address} Y: {*(float*)address + 4}");
                Console.WriteLine($"X: {address} Y: {address + 4}");
            }

            var vector3 = new Vector3(1, 2, 3);
            var vector3Custom = new Vector3Custom { x = vector3.X, y = vector3.Y, z = vector3.Z };
            address = GetVector3Address(ref vector3Custom);
            unsafe
            {
                Console.WriteLine($"X: {*(float*)address} Y: {*(float*)address + 4} Z: {*(float*)address + 8}");
                Console.WriteLine($"X: {address} Y: {address + 4} Z: {address + 8}");
            }

            var vector4 = new Vector4(1, 2, 3, 4);
            var vector4Custom = new Vector4Custom { x = vector4.X, y = vector4.Y, z = vector4.Z, w = vector4.W };
            address = GetVector4Address(ref vector4Custom);
            unsafe
            {
                Console.WriteLine($"X: {*(float*)address} Y: {*(float*)address + 4} Z: {*(float*)address + 8} W: {*(float*)address + 12}");
                Console.WriteLine($"X: {address} Y: {address + 4} Z: {address + 8} W: {address + 12}");
            }

            int a = 1000;
            address = GetIntAddress(a);
            Console.WriteLine($"X: {address.ToString("X8")}");

            float b = 1000;
            address = GetFloatAddress(b);
            Console.WriteLine($"X: {address}");

            double c = 1000;
            address = GetDoubleAddress(c);
            Console.WriteLine($"X: {address}");
        }


        [StructLayout(LayoutKind.Sequential)]
        private struct Vector2Custom
        {
            public float x;
            public float y;
        }

        [StructLayout(LayoutKind.Sequential)]
        private struct Vector3Custom
        {
            public float x;
            public float y;
            public float z;
        }


        [StructLayout(LayoutKind.Sequential)]
        private struct Vector4Custom
        {
            public float x;
            public float y;
            public float z;
            public float w;
        }
    }
}

    
```
